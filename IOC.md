/*
**--의존성 역전--**
의존성 역전은 객체 간의 결합도를 줄이고 
유연한 코드를 작성하게 하여 가독성 및 코드의 중복, 유지보수를 편하게 할 수 있게 한다.

객체간의 결합도(Coupling)
어떤 특정 객체가 존재하기 위해 꼭 존재해야 하는 것 그리고 그 관계를 의존성이라고 한다.
예를 들어게임에서 Player는 무기를 꼭 필요로 하기 때문에 Weapon 클래스 객체를 꼭 가지고 있어야 한다.
이러한 관계를 위에 언급한 것 처럼 의존성이라고 한다.

의존성은 코드 상에서 new 키워드로서 객체간의 의존성이 생성된다.

ex)
class Player {
    private Weapon weapon;
    Player(){
    }
    void setWeapon(){
        this.weapon = new Weapon();
    }    
}

이러한 방식은 객체간의 강결합으로 묶여지면서 코드의 유연성을 떨어트리고 
코드의 중복 및 가독성을 떨어뜨리는 원인이 된다.

Weapon 클래스에 Weapon만이 아니라 칼, 총 등 여러 종류가 있다면 중복적으로 적어줘야 되므로
이 코드의 유연성을 확보하는 방법으로는 의존성 역전을 이용하면 된다.

그 예시로는 아래와 같다
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
        // TODO Auto-generated method stub
        Player player = new Player();

        player.setWeapon(new Gun());
        player.usePlayerWeapon();

        player.setWeapon(new Spike());
        player.usePlayerWeapon();

        player.setWeapon(new Knife());
        player.usePlayerWeapon();
    }
}

    // Result : 
    Use Gun
    Use Spike
    Use Knife

위와 같이 코드가 설계되면 interface에 맞춰서 구현된 무기들의 인스턴스를 갈아 끼우면 되므로
코드가 유연해지고 가독성이 높아지며 중복이 제거된다.

**--IoC** 컨테이너--
스프링에서는 위와 같은 Knife, Gun 등을 컨테이너라는 곳에서 Bean이라는 인스턴스 형태로 관리한다.
xml이나 java config 파일로부터 설정값들을 입력한 후 이 정보를 토대로 스프링이 컨테이너를
생성하여 설정 파일들에 등록되어 있는 Bean 객체들을 관리한다.

각 Bean이 가지고 있는 의존성 설정파일에 입력해둔 정보를 토대로 컨테이너가 생설될 시
자동적으로 해당 의존성을 주입해준다(의존성 역전(IoC) 원칙을 지킨다는 가정하에)

이것을 스프링에서는 해당 컨테이너를 IoC 컨테이너라고 부르고 이런 의존성을 주입시키는 행위를 
DI(Dependecny Injection) 이라고 한다.

*/