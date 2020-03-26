```
스프링부트(Spring Boot) HTTPS 구축 

스프링부트에서 HTTPS 설정법은 다음과 같습니다.

Terminal 창에 다음과 같이 커맨드를 입력하여 keystore 파일을 하나 생성합니다.

keytool -genkey -alias spring -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 4000


다음 알맞게 keystore에 대한 정보를 입력합니다.
(개인정보)

application.properties에 위에서 설정한 정보를 입력합니다.

# application.properties
server.ssl.key-store=keystore.p12
server.ssl.key-store-type=PKCS12
server.ssl.key-store-password=123456
server.ssl.key-alias=spring
위 https로 설정된 스프링 부트 어플리케이션에 http://localhost:8080/ 로 요청했을 경우에는 요청을 받지 않는다는 브라우져 메세지가 뜨게 됩니다.


그렇다면 https 프로토콜로 위와 같은 요청을 했을 경우(https://localhost:8080)에는 바로 브라우져가 작동할까요? 그렇지 않습니다. 브라우저는 신뢰할 수 있는 인증기관이 만든 인증서에 대한 공인키(pub-key)의 리스트는 알고 있지만 위에서 작성한 정보에 대해서는 전혀 모르는 상태이기 때문에 아래의 경고 신호를 주는 것입니다. 하지만 이미 위에서 만든 어플리케이션이라는 것을 알고 있기 때문에 바로 접속해도 무방합니다.

| 스프링부트(Spring Boot) 다중 커넥터 설정 


스프링부트의 톰캣 내장 서버는 기본적으로 커넥터가 한 개로 설정되어 있습니다. 따라서 위의 https 요청을 받는 것과 더불어 http 프로토콜로도 요청을 받기 위해서는 커넥터를 하나 더 만들어야 합니다. 아래는 스프링 부트에서 코드를 통해 커넥터를 하나 더 만드는 것을 나타낸 예제입니다.
import org.apache.catalina.connector.Connector;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.web.embedded.tomcat.TomcatServletWebServerFactory;
import org.springframework.boot.web.servlet.server.ServletWebServerFactory;
import org.springframework.context.annotation.Bean;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;


@SpringBootApplication
@RestController
public class Application {

    @GetMapping("/hello")
    public String hello(){
        return "Hello Spring Boot";
    }

    public static void main(String[] args)  {
        SpringApplication application = new SpringApplication(Application.class);
        application.run(args);
    }

    @Bean
    public ServletWebServerFactory serveltContainer(){
        TomcatServletWebServerFactory tomcat = new TomcatServletWebServerFactory();
        tomcat.addAdditionalTomcatConnectors(createStandardConnector());
        return tomcat;
    }

    private Connector createStandardConnector(){
        Connector connector = new Connector("org.apache.coyote.http11.Http11NioProtocol");
        connector.setPort(8070);
        return connector;
    }
}
# application.properties
server.ssl.key-store=keystore.p12
server.ssl.key-store-type=PKCS12
server.ssl.key-store-password=123456
server.ssl.key-alias=spring
server.port=8443
위 코드와 설정 파일을 보면 https 는 8443(https://localhost:8443/hello), http는 8070 (http://localhost:8070/hello)으로 받는 것을 나타냅니다.



| 스프링부트(Spring Boot) HTTP2 설정 및 구축

스프링부트에서는 톰캣 내장서버를 기반으로한 http2 프로토콜을 설정할 수 있습니다. 하지만 여기서 주의해야 할 것은 jdk8 버전 이하에서는 특별한 설정을 하지 않을 경우 다음과 같은 에러 메세지를 내면서 http1.1 프로토콜로 서버가 동작하게 된다는 것입니다.

ERROR 13336 --- [           main] o.a.coyote.http11.Http11NioProtocol      : The upgrade handler [org.apache.coyote.http2.Http2Protocol] for [h2] only supports upgrade via ALPN but has been configured for the ["https-jsse-nio-8443"] connector that does not support ALPN.
이 문제를 해결하기 위해서는 jdk를 9버전 이상으로 업데이트하거나 아니면 libtcnative library를 설치하여 의존성을 추가해야 합니다. 여기서는 jdk 9버전 이상이라 가정하여 http2 프로토콜을 설정하는 방법을 알아보겠습니다. 



다음과 같이 application.properties 파일에 다음과 같이 설정값을 추가하면 됩니다. 여기서 중요한 것은 https가 설정이 되있어야 http2를 설정할 수 있다는 것입니다.

# application.properties
server.ssl.key-store=keystore.p12
server.ssl.key-store-type=PKCS12
server.ssl.key-store-password=123456
server.ssl.key-alias=spring
server.port=8443
server.http2.enabled=true # http2 설정



```