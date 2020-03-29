```
스프링부트 테스트 ( Spring Boot Test )



스프링부트에서는 @SpringBootTest 어노테이션을 통해 스프링부트 어플리케이션 테스트에 필요한 거의 모든 의존성을 제공해 줍니다. 또한 @SpringBootTest 어노테이션 내에 어떠한 테스트 환경으로 테스트를 실행할 것인지를 따로 지정할 수 있습니다.



스프링부트 테스트를 진행하기 위해서는 먼저 다음과 같이 의존성을 추가해야 합니다.

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>


테스트를 실행하기 위해 다음과 같이 간단한 컨트롤러와 서비스를 작성한 다음 스프링부트 어플리케이션이 실행될 메인 진입점이 될 클래스를 작성합니다. 



아래는 테스트 해보고자 하는 프로젝트 구조를 나타낸 것입니다.

+---src
|   +---main
|   |   +---java
|   |   |   \---com
|   |   |       \---tutorial
|   |   |           \---springboot
|   |   |               |   Application.java
|   |   |               |
|   |   |               +---controller
|   |   |               |       SampleController.java
|   |   |               |
|   |   |               \---service
|   |   |                       SampleService.java
|   |   |
|   \---test
|       +---java
|       |   \---com
|       |       \---tutorial
|       |           \---springboot
|       |                   SampleSpringBootTest.java

다음은 관련 코드들입니다.

@RestController
public class SampleController {

    @Autowired
    private SampleService sampleService;

    @GetMapping("/hello")
    public String hello() {
        return "hello " + sampleService.getName();
    }
}
@Service
public class SampleService {

    public String getName(){
        return "saelobi";
    }
}
@SpringBootApplication
public class Application {

    public static void main(String[] args)  {
        SpringApplication application = new SpringApplication(Application.class);
        application.run(args);
    }
}


다음 위에서 작성한 코드들을 테스트할 테스트 코드를 작성합니다.

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.MOCK)
@AutoConfigureMockMvc
public class SampleSpringBootTest {

    @Autowired
    MockMvc mockMvc;

    @Test
    public void hello() throws Exception {
        mockMvc.perform(get("/hello"))
                .andExpect(status().isOk())
                .andExpect(content().string("hello saelobi"))
                .andDo(print());
    }
}
위 코드에 대한 설명은 다음과 같습니다.

@RunWith 어노테이션은 JUnit 프레임워크가 테스트를 실행할 시(JUnit은 내장된 Runner를 테스트 시 실행하고 됨) 테스트 실행방법을 확장할 때 쓰는 어노테이션 입니다. 쉽게 말해 JUnit 프레임워크가 내장된 Runner를 실행할 때 @Runwith 어노테이션을 통해 SpringRunner.class라는 확장된 클래스를 실행하라고 지시한 것입니다.
@SpringBootTest는 스프링 부트 어플리케이션 테스트 시 테스트에 필요한 거의 모든 의존성을 제공 어노테이션입니다. @SpringBootApplication을 기준으로 스프링 빈을 등록함과 동시에 Maven 같은 빌드 툴에 의해 추가된 스프링부트 의존성도 제공해 줍니다. @SpringBootTest 어노테이션에는 webEnvironment라는 값을 통해 웹 어플리케이션 테스트시 Mock으로 테스트할 것인지 실제 톰캣 같은 서블릿 컨테이너를 구동해서 테스트할 것인지를 정할 수 있습니다.
@AutoConfigureMockMvc는 Mock 테스트시 필요한 의존성을 제공해줍니다.
MockMvc 객체를 통해 실제 컨테이너가 실행되는 것은 아니지만 로직상으로 테스트를 진행할 수 있습니다. (DispatcherServlet은 로딩되어 Mockup으로서 기능합니다)
print() 함수를 통해 좀 더 디테일한 테스트 결과를 볼 수 있습니다.

MockHttpServletRequest:
HTTP Method = GET
Request URI = /hello
Parameters = {}
Headers = {}
Body = null
Session Attrs = {}

Handler:
Type = com.tutorial.springboot.controller.SampleController
Method = public java.lang.String com.tutorial.springboot.controller.SampleController.hello()

Async:
Async started = false
Async result = null

Resolved Exception:
Type = null

ModelAndView:
View name = null
View = null
Model = null

FlashMap:
Attributes = null

MockHttpServletResponse:
Status = 200
Error message = null
Headers = {Content-Type=[text/plain;charset=UTF-8], Content-Length=[13]}
Content type = text/plain;charset=UTF-8
Body = hello saelobi
Forwarded URL = null
Redirected URL = null
Cookies = []
2019-01-01 14:06:16.853  INFO 6284 --- [       Thread-2] o.s.s.c.ThreadPoolTaskExecutor           : Shutting down ExecutorService 'applicationTaskExecutor'


| 서블릿 컨테이너 테스트


위에서 진행한 Mockup을 통한 테스트가 아닌 실제 서블릿 컨테이너를 구동 후 테스트 하기 위해서는 다음과 같이 @SpringBootTest 어노테이션에 webEnvironment값을 변경해 줘야 합니다.



또한 Mockup 테스트가 아니기 때문에 MockMvc 객체를 통해서가 아닌 TestRestTemplate 객체 같은 다른 방식으로 테스트를 해줘야 합니다. 

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class SampleSpringBootTest {

    @Autowired
    TestRestTemplate testRestTemplate;

    @Test
    public void hello() throws Exception {
        String result = testRestTemplate.getForObject("/hello", String.class);
        assertThat(result).isEqualTo("hello saelobi");
    }
}


만일 테스트를 하고자 하는 웹 어플리케이션들을 구성하는 클래스들이 무거워서 간단히 컨트롤러만을 테스트하고 싶다면은 다음과 같이 SampleService를 이용하여 서비스단을 Mockup으로 만들고 테스트할 수 있습니다.

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class SampleSpringBootTest {

    @Autowired
    TestRestTemplate testRestTemplate;

    @MockBean
    SampleService sampleService;

    @Test
    public void hello() throws Exception {
        when(sampleService.getName()).thenReturn("saelobi");

        String result = testRestTemplate.getForObject("/hello", String.class);
        assertThat(result).isEqualTo("hello saelobi");
    }
}
이 밖에도 다른 웹 단을 테스트하고 싶으면 해당 샘플 객체를 통해서 Mockup을 만들어 테스트할 수 있습니다.



| WebTestClient 테스트

스프링부트 웹 어플리케이션 테스트 시 웹 클라이언트를 통해서 비동기 형식으로 테스트를 진행할 수 있습니다. 이 때 webflux에 대한 의존성이 추가되어야 합니다.

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>


다음은 WebTestClient를 이용하여 비동기 형식으로 테스트를 진행하는 테스트 코드입니다.

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class SampleSpringBootTest {

    @Autowired
    WebTestClient webTestClient;

    @MockBean
    SampleService sampleService;

    @Test
    public void hello() throws Exception {
        when(sampleService.getName()).thenReturn("saelobi");

        webTestClient.get().uri("/hello").exchange()
                .expectStatus().isOk()
                .expectBody(String.class).isEqualTo("hello saelobi");
    }
}


| 슬라이스 테스트 어노테이션

SpringBootTest는 수많은 스프링 빈을 등록하여 테스트에 필요한 의존성을 추가해줍니다. 따라서 이 수많은 빈들을 등록하지 않고 필요한 빈만을 등록하여 테스트를 등록하고자 하면 슬라이스 테스트 어노테이션을 통해 테스트를 진행해야 합니다.

@RunWith(SpringRunner.class)
@WebMvcTest(SampleController.class)
public class SampleSpringBootTest {

    @Autowired
    MockMvc mockMvc;

    @MockBean
    SampleService sampleService;

    @Test
    public void hello() throws Exception {
        when(sampleService.getName()).thenReturn("saelobi");

        mockMvc.perform(get("/hello"))
                .andExpect(content().string("hello saelobi"));
    }
}
위에 @WebMvcTest 어노테이션을 등록하게 되면 웹 테스트를 하는 데 필요한 @Controller, @ControllerAdvice, @JsonComponent, Convert 등의 어노테이션만 등록되게 됩니다. 이 밖에 테스트를 하는 데 필요하지 않은 어노테이션은 등록되지 않습니다. 따라서 웹 테스트 말고 다른 테스트를 하고자 할 때는 직접 의존성을 추가해야하는 번거로움이 있습니다.



| OutputCapture 사용하기


스프링부트에서는 OutputCature 객체를 통해 콘솔에 출력되는 로깅 메세지를 테스트할 수 있는 방법을 제공합니다. 

다음과 같이 컨트롤러 클래스를 수정합니다.

@RestController
public class SampleController {

    Logger logger = LoggerFactory.getLogger(SampleController.class);

    @Autowired
    private SampleService sampleService;

    @GetMapping("/hello")
    public String hello() {
        logger.info("logging output test");
        System.out.println("standard output test");
        return "hello " + sampleService.getName();
    }
}


다음 테스트 코드는 로깅 메세지 및 표준 출력을 테스트하도록 수정합니다.

@RunWith(SpringRunner.class)
@WebMvcTest(SampleController.class)
public class SampleSpringBootTest {

    @Rule
    public OutputCapture outputCapture = new OutputCapture();

    @Autowired
    MockMvc mockMvc;

    @MockBean
    SampleService sampleService;

    @Test
    public void hello() throws Exception {
        when(sampleService.getName()).thenReturn("saelobi");

        mockMvc.perform(get("/hello"))
                .andExpect(content().string("hello saelobi"));

        assertThat(outputCapture.toString())
                .contains("logging output test")
                .contains("standard output test");
    }
}


```