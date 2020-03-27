```
| CORS(Cross-Origin Resource Sharing)이란



CORS는 동일한 출처(Origin: 최초 자원이 서비스된 출처)가 아니여도 다른 출처에서의 자원을 요청하여 쓸 수 있게 허용하는 구조를 뜻합니다.
보통 보안 상의 이슈(DOM을 통한 취약한 데이터 접근 시도) 때문에 동일 출처(Single Origin Policy)를 기본적으로 웹에서는 준수하게 됩니다. 따라서 최초 자원을 요청한 출처 말고 다른 곳으로 스크립트를 통해 자원을 요청하는 것은 금지됩니다.
CORS을 적용하려면 웹 어플리케이션에 그에 따른 처리를 해야하고 스프링 부트에서는 @CrossOrigin 어노테이션 혹은 WebConfig를 통해 CORS를 적용하는 방법을 제공합니다.


| 기존 Single Origin Policy



프로젝트를 두개 생성하여 하나는 클라이언트 쪽에서 직접 리소스를 요청하는 웹 어플리케이션 다른 하나는 ajax를 통해 다른 출처에서 자원을 요청할 때 그 자원을 제공하는 웹 어플리케이션을 만듭니다.



프로젝트 구조( 직접 리소스를 요청받는 웹 어플리케이션 )

// SpringClientApplication
|   pom.xml
+---src
|   +---main
|   |   +---java
|   |   |   \---com
|   |   |       \---tutorial
|   |   |           \---springclient
|   |   |                   SpringClientApplication.java
|   |   |
|   |   \---resources
|   |       |   application.properties
|   |       |
|   |       +---static
|   |       |       index.html
|   |       |
|   |       \---templates


HTML 코드

<!--index.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Cors Client</h1>
    <script src="/webjars/jquery/3.3.1/dist/jquery.min.js"></script>
    <script>
        $(function(){
            $.ajax("http://localhost:8080/hello")
                .done(function(msg){
                    alert(msg);
                })
                .fail(function(){
                    alert("fail");
                })
        })
    </script>
</body>
</html>
스크립트 태그에서 ajax를 통해 다른 출처인 http://localhost:8080/hello 의 자원을 요청합니다. 만일 요청을 실패했을 경우 fail 메세지를 띄웁니다.


properties 파일

server.port=18080
포트는 18080으로 설정했습니다.


소스코드

@SpringBootApplication
@RestController
public class SpringClientApplication {

    @GetMapping("/hello")
    public String hello(){
        return "hello";
    }

    public static void main(String[] args) {
        SpringApplication.run(SpringClientApplication.class, args);
    }

}


프로젝트 구조( ajax를 통해 자원을 요청받는 웹 어플리케이션 )

// SpringBootTutorialApplication
|   pom.xml
+---src
|   +---main
|   |   +---java
|   |   |   \---com
|   |   |       \---tutorial
|   |   |           \---springboottutorial
|   |   |                   SampleController.java
|   |   |                   SpringBootTutorialApplication.java
|   |   |
|   |   \---resources
|   |       |   application.properties
|   |       |
|   |       +---static
|   |       \---templates


소스코드

@SpringBootApplication
public class SpringBootTutorialApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBootTutorialApplication.class, args);
    }

}
@RestController
public class SampleController {

    @GetMapping("/hello")
    public String hello(){
        return "hello";
    }
}


기본적으로 Single Origin Policy를 지키고 있기 때문에 스크립트를 통해 다른 출처에 있는 자원을 획득하지 못합니다.


| CORS가 적용된 웹 어플리케이션(@CrossOrigin)

소스 코드

@RestController
public class SampleController {

    @CrossOrigin(origins="http://localhost:18080")
    @GetMapping("/hello")
    public String hello(){
        return "hello";
    }
}
@CorssOrigin을 통해 해당 출처에서도 스크립트를 통해 자원을 획득할 수 있도록 허용합니다.



| CORS가 적용된 웹 어플리케이션(WebConfig )



프로젝트 구조

|   pom.xml
+---src
|   +---main
|   |   +---java
|   |   |   \---com
|   |   |       \---tutorial
|   |   |           \---springboottutorial
|   |   |                   SampleController.java
|   |   |                   SpringBootTutorialApplication.java
|   |   |                   WebConfig.java
|   |   |
|   |   \---resources
|   |       |   application.properties
|   |       |
|   |       +---static
|   |       \---templates


소스 코드

@RestController
public class SampleController {

    @GetMapping("/hello")
    public String hello(){
        return "hello";
    }
}
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://localhost:18080");
    }
}
모든 URL에 출처가 http://localhost:18080에 대한 스크립트를 통한 자원 요청을 허용하는 설정 코드입니다.
결과는 위와 같습니다.


```