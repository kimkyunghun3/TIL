```

도대체 왜 getter와 setter 굳이 왜 쓰는지? 왜 써야하는거지?

예제는 ES6 기준으로 진행하지만, 언어와 상관없이 봐도 무관하다.


getter와 setter를 언급한다면, 대부분 private 개념이 따라오게 된다.

책이나 글에서 볼 수 있는 극단적인 예는 아래와 같다.

private 변수를 지정한 후, 이 변수에 접근하기 위해 getter, setter를 이용한다.

맞는 말이다. 하지만 이해하기 힘들 거라고 생각한다.


다음 예제를 통해 확인해보자.

1. name을 저장할 때는 정확한 값일 때 저장한다.

2. name을 가져올 때는 대문자로 된 이름을 얻을 수 있다.


위 특징을 가지는 Person 클래스를 만들어보자.


class Person {

    constructor(name, age) {
        this._name = name;
        this.age = age;
    }

    get name() {
        return this._name.toUpperCase();
    }

    set name(newName){
        if(newName){ 
            this._name = newName;
        }
    }

}

let man = new Person('John', 10);
console.log(man.name, man.age);
man.name = 'John Park';
man.age = 20;
console.log(man.name, man.age);



이름이라는 변수는 실제 _name이 된다.

코드를 보면 실제 데이터인 _name에 직접 접근하지 않으면서, 정의된 오퍼레이션을 통해서만 접근하고 있다.



또한, 이름을 얻을 때, 사용자는 단순히 이름을 얻을 뿐이다.

대문자로 가공하는 과정은 내부에서 일어날 뿐이다.

즉, 단순히 사용자는 이름을 얻고자 할뿐, 얻는 과정에 있는 내부적인 일은 신경쓰지 않는다.

이러한 원리가 캡슐화의 이점인 정보 은닉이 된다.



메소드로 접근하는 것처럼 보이지 않기 때문에 외관상에도 좋다.

이건 자바스크립트의 특징이기에, 아마 Java와 C++의 경우는 불가능할 것이다.

(사실 상 this._name에 직접 접근할 수 있지만, 배제하자)



조금 더 나아가, 다른 예제를 통해 getter, setter를 통한 일관성 유지에 관한 예를 들어본다.

start, end, duration 3개의 변수가 있는 클래스가 존재한다.

start - 시작하는 시간
end - 끝나는 시간
duration - 지속되는 시간


먼저 getter, setter를 쓰지 않고 변수에 직접 접근하는 예를 보자.



class Time {

    constructor(start, end) {
        this._start = start;
        this._end = end;
        this._duration = end - start; 
    }

}

const time = new Time(0, 20);

time._start = 5;
time._duration -= 5;

console.log(time._start)



start 변수의 값을 수정할 때, 사실상 duration 변수도 수정되어야하기 때문에 위와 같은 코드가 나올 것이다.

이 경우, 변수의 직접 접근을 통해 보호되지 못한다.

그 결과, 누구나 접근하여 변경할 수 있기에, start에 따른 duration 값이 맞지 않는 결과가 초래될 수 있다.

즉, 변수 관계에 있어서, 일관성을 깨뜨리게 된다.



getter, setter를 사용한 예를 보자.



class Time {

    constructor(start, end) {
        this._start = start;
        this._end = end;
        this._duration = end - start 
    }

    setStart (newStart) {
        this._start = newStart;
        this._duration = this._end - this._start; 
    }

    getStart() {
        return this._start;
    }

}

const time = new Time(0, 20);

time.setStart(5);
console.log(time.getStart());



getter, setter를 통해 접근함으로써, 변수를 보호할 수 있다.

또한, setter를 통해 start와 duration을 설정함으로써, 위에서 발생한 일관성 문제를 해결할 수 있다.



자바스크립트만의 getter, setter를 사용해보자.

변수에 직접 접근하는 것처럼 보이지만 내부적으로는 그렇지 않다.

위 예시보다 일관성 유지에 맞는 코드 및 외관상으로도 보기 좋은 유연한 코드가 만들어진다.



class Time {

    constructor(start, end) {
        this._start = start;
        this._end = end;
        this._duration = end - start; 
    }

    set start (newStart) {
        this._start = newStart;
        this._duration = this._end - this._start; 
    }

    get start () {
        return this._start;
    }

}

const time = new Time(0, 20);

time.start = 5;
console.log(time.start);



getter, setter는 위의 예들처럼 특정 목적이 있는 경우 설정한다.

무조건적으로 쓴다면, 단순히 불필요한 코드가 늘어나는 것이다.

```