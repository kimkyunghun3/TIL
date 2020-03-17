```
스프링 부트 의존성 관리 (Spring Boot Dependency Management)

스프링 부트는 Maven, Gradle 같은 빌드 관리 툴을 통해 의존성을 관리한다
여기서는 Maven 기준으로 스프링 부트가 의존성을 어떻게 관리하는 지 살펴보도록 하겠다.

pom.xml 에 스프링 부트에 대한 기본적인 의존성을 추가하면 다음과 같다

<parent>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-parent</artifactId>
<version>2.1.1.RELEASE</version>
</parent>

<dependencies>
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-test</artifactId>
<scope>test</scope>
</dependency>
</dependencies>

다음과 같이 의존성을 추가하면 스프링 부트가 자체적으로 관리하는 의존성이 자동적으로 상속된다.
그 이유는 spring-boot-starter-parent 아티팩트를 parent 태그에 명시하면 
spring-boot-dependencies-x.x.x.RELEASE.pom 파일이 상속되어 
사용자가 특별히 명시하지 않아도 스프링 부트에서 제공하는 의존성이 자동적으로 설정되기 때문입니다.

인텔리제이(IntelliJ) 기준으로 pom.xml의 dependency의 상속 여부를 판단하는 방법은
에디터 왼쪽의 아이콘을 참조하면 됩니다.

Maven의 의존성 관리 상황을 쉽게 확인할 때는 인텔리제이 IDE 오른쪽에 Maven 아이콘을 클릭하여 확인하면 됩니다.

만일 spring-boot-starter-parent 로 상속받은 설정 정보를 다시 재정의하고 싶으면
다음과 같이 properties 태그에 명시하면 됩니다. 

<properties>
    <spring.version>5.0.6.RELEASE</spring.version>
</properties>
그리고 스프링 부트에서 자체적으로 제공하지 않는 의존성(spring-boot-dependencies-x.x.x.RELEASE.pom 목록에 없는)은 pom.xml에 명시해야 합니다. 

<dependency>
    <groupId>org.modelmapper</groupId>
    <artifactId>modelmapper</artifactId>
    <version>2.1.0</version>
</dependency>



```