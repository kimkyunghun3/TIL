**의존성 주입 DI(Dependency Injection)**


의존성 주입은 객체가 필요로 하는 어떤 객체를 생성자(Constructor) 혹은 새터(Setter)를
통해서 주입하는 것을 말한다.

강결합으로 어마어마한 유지보수 비용 때문에 의존성 주입이 필요하다.

일체형 배터리와 분리형 배터리에서 어떤 것이 나중에 배터리를 갈아끼울 때 더 편리할 것인가? 
이 갈아끼운다는 의미는 결국에는 소프트웨어에서 말하는 유지보수다. 
그리고 일체형 배터리에서 기계와 배터리와의 관계는 강결합 관계이다.
나중을 생각하면 이 둘을 교체할 것을 대비했을 때 둘의 관계를 약하게 하는 것이 맞다.

다음 코드는 Player 객체에 있는 Weapon이라는 의존성 주입을 새터를 통해서 하고 있다.
Gun으로 하든 Spike로 하든 무기를 바꿀 때 그 무기 객체를 생성하고 단순히 주입하기만 하면 된다.

class Knife implements Weapon{

    public void useWeapon() {
        System.out.println("Use Knife");
    }
}

class Gun implements Weapon{

    public void useWeapon() {
        System.out.println("Use Gun");
    }
}

class Spike implements Weapon{

    public void useWeapon() {
        System.out.println("Use Spike");
    }
}

interface Weapon {

    void useWeapon();
}

public class Player {

    private Weapon weapon;

    Player(){
    }

    public void setWeapon(Weapon weapon) {
        this.weapon = weapon;
    }

    public void usePlayerWeapon() {
        weapon.useWeapon();
    }
}

public class Main {

    public static void main(String[] args) {
        /**
         * 의존성 주입을 통해 의존 요소들을 쉽게 갈아 끼울 수 있다.
         */
        Player player = new Player();

        player.setWeapon(new Gun());   // Player에 Gun 객체를 통한 의존성 주입
        player.usePlayerWeapon();

        player.setWeapon(new Spike()); // Player에 Spike 객체를 통한 의존성 주입
        player.usePlayerWeapon();

        player.setWeapon(new Knife()); // Player에 Knife 객체를 통한 의존성 주입
        player.usePlayerWeapon();
    }
}

**스프링을 통한 컨테이너 생성 및 의존성 주입(Spring, Container, DI)**

스프링에서는 xml 혹은 java config, annotation을 통해서 
컨테이너 설정 정보 및 bean객체 그리고 의존성 관계 정보를 입력할 수 있다. 
여기서 bean은 스프링 컨테이너 상에서 생성된 객체라고 보면 된다.
또한 컨테이너는 스프링에서 IoC 원칙을 통한 객체와 그 의존성들을 관리하기 위해 만든 요소다.
bean객체들이 들어가있는 통이라고 쉽게 생각해도 된다.

이 bean은 상술했듯이 IoC 컨테이너 상에서 관리된다. 
스프링 설정파일에 등록된 bean은 프로그램 실행 도중에 바꿀 수 없다.
위 코드를 스프링에서 xml 파일 설정방법을 이용해서 똑같이 구현해볼 것이다.

bean을 생성할 때 id와 class 정보를 입력해야 한다. id는 이 bean의 식별자이며
classs는 이 스프링 객체인 bean의 클랫르르 지정하는 속성이다.

<-- appContext.xml -->
<-- 스프링 xml 설정파일 -->
<?xml version="1.0" encoding="UTF-8"?>
/*
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="gun" class="com.tutorial.spring.Gun"/>
    <bean id="knife" class="com.tutorial.spring.Knife"/>
    <bean id="spike" class="com.tutorial.spring.Spike"/>

    <bean id="gunPlayer" class="com.tutorial.spring.Player">
        <constructor-arg ref="gun"/>
    </bean>
    <bean id="knifePlayer" class="com.tutorial.spring.Player">
        <property name="weapon" ref="knife"/>
    </bean>
    <bean id="spikePlayer" class="com.tutorial.spring.Player">
        <property name="weapon" ref="spike"/>
    </bean>


속성을 주입하는 것은 두 방법이 있다. 생성자를 통한 방법과 새터(Setter)를 통한 방법이다.
생성자를 통한 방법은 <constructor-arg>, 새터를 통한 방법은 <property> 태그를 통해 정보를 입력한다.
주입할 bean 객체의 정보는 ref="[ID명]"을 속성에 입력하면 된다.

스프링 컨테이너의 bean객체에 접근할 때는 getBean을 쓴다. 
이 때, getBean에 클래스 정보를 입력하면 번거롭고 불필요한 Type-casting을 하지 않아도 된다.