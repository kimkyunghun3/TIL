```

@Configuration 어노테이션을 등록하여 Autoconfigure 스프링 부트 자동 설정을 만들었지만 여기에 문제점이 있습니다.

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication application = new SpringApplication(Application.class);
        application.setWebApplicationType(WebApplicationType.NONE);
        application.run(args);
    }

    @Bean
    public Saelobi saelobi(){
        Saelobi saelobi = new Saelobi();
        saelobi.setName("KBS2");
        saelobi.setHowLong(50);
        return saelobi;
    }
}
@Component
public class AppRunner implements ApplicationRunner {

    @Autowired
    Saelobi saelobi;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        System.out.println(Saelobi.class);
        System.out.println(saelobi);
    }
}


만일 @EnableAutoConfiguration 어노테이션을 통한 스프링 빈이 주입되었을 경우 어떤 특별한 이유로 이 빈을 다시 재정의하여 쓸 시에는 다음과 같은 에러 문구가 뜨면서 재정의 시도가 차단됩니다.

***************************
APPLICATION FAILED TO START
***************************

Description:

The bean 'saelobi', defined in class path resource [com/tutorial/AutoConfig.class], could not be registered. A bean with that name has already been defined in com.tutorial.springboot.Application and overriding is disabled.

Action:

Consider renaming one of the beans or enabling overriding by setting spring.main.allow-bean-definition-overriding=true


| @ConditionalOnMissingBean을 통한 충돌 요소 해결


위 오버라이딩 충돌을 해소하려면 자동 설정 부분을 Maven 프로젝트를 통해 만들시 @ConditionalOnMissingBean 어노테이션을 추가해야합니다.
이 어노테이션은 스프링 부트 프로젝트 상에서 동명의 스프링 빈이 정의되었을 시에는 쓰지 않고 그 스프링 빈을 쓰며 만약 없을 시에는 자동 등록한 빈을 쓰게 끔 유도하는 용도로 쓰입니다.

@Configuration
public class AutoConfig {

    @Bean
    @ConditionalOnMissingBean
    public Saelobi saelobi(){
        Saelobi saelobi = new Saelobi();
        saelobi.setHowLong(5);
        saelobi.setName("KBS");
        return saelobi;
    }
}
다시 mvn install 을 실행하여 local repository에 등록할 경우
이번에는 충돌했던 부분이 해소되고 스프링 부트에 등록됬던 saelobi 빈이 주입되는 것을 알 수 있습니다.

class com.tutorial.Saelobi
Saelobi{name='KBS2', howLong=50}


| @ConfigurationProperties를 통한 자동 설정 클래스 만들기



자동 설정 클래스 내의 스프링 빈을 재정의 할 때 코드 상에서가 아닌 property 파일을 통해 재정의 하고자 할 때는 
@ConfigurationProperties 어노테이션을 통해 설정파일로도 재정의가 가능하도록 코드를 작성해야 합니다.







먼저 pom.xml에 다음과 같은 dependency를 추가해야 합니다.

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
public class Saelobi {

    String name;

    int howLong;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getHowLong() {
        return howLong;
    }

    public void setHowLong(int howLong) {
        this.howLong = howLong;
    }

    @Override
    public String toString() {
        return "Saelobi{" +
                "name='" + name + '\'' +
                ", howLong=" + howLong +
                '}';
    }
}


다음 property 파일을 통해 값을 가져오는 역할을 하는 클래스를 작성합니다.

@ConfigurationProperties("saelobi")
public class SaelobiProperties {

    private String name;

    private int howLong;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getHowLong() {
        return howLong;
    }

    public void setHowLong(int howLong) {
        this.howLong = howLong;
    }
}


다음 @EnableConfigurationPropertes 어노테이션을 통해 위 클래스를 프로퍼티 파일 정보를 담고 있는 클래스로 자동 등록하게 합니다.

@Configuration
@EnableConfigurationProperties(SaelobiProperties.class)
public class AutoConfig {

    @Bean
    @ConditionalOnMissingBean
    public Saelobi saelobi(SaelobiProperties properties){
        Saelobi saelobi = new Saelobi();
        saelobi.setHowLong(properties.getHowLong());
        saelobi.setName(properties.getName());
        return saelobi;
    }
}


mvn install을 한 후 위 프로젝트를 local repository에 등록합니다.


| Property 파일을 통한 자동 설정 스프링 빈을 재정의


다음과 같은 스프링 부트 구조를 만듭니다. 여기서 중요한 것은 application.properties 파일의 존재입니다.

# application.properties
saelobi.name = KBS_NEW
saelobi.how-long = 90

위 Maven 프로젝트를 통해 만든 dependency 추가는 다음과 같습니다. 

<dependency>
    <groupId>com.tutorial</groupId>
    <artifactId>autoconfigure</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>


이제 어플리케이션을 실행하면 application.properties에 설정한 값을 읽어와 saelobi 빈을 재정의하게 됩니다.

@Component
public class AppRunner implements ApplicationRunner {

    @Autowired
    Saelobi saelobi;

    @Override
    public void run(ApplicationArguments args) throws Exception {
        System.out.println(Saelobi.class);
        System.out.println(saelobi);
    }
}
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication application = new SpringApplication(Application.class);
        application.setWebApplicationType(WebApplicationType.NONE);
        application.run(args);
    }
}
class com.tutorial.Saelobi
Saelobi{name='KBS_NEW', howLong=90}


```