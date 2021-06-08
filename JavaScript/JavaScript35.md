# [드림코딩 by 엘리] JavaScript 기초 강의(5) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/513) 참고**



# class와 object

## class

* 연관있는 데이터(변수, 함수)를 한 곳에 묶어놓는 컨테이너

* 속성(filed), 행동(method)로 이루어져 있다.
```JavaScript
class person {
// filed
name;
age;
// method
speak();
}
```

* data class: filed만 들어있는 클래스

* 클래스 안에서 내부적으로 보여지는 변수와 밖에서 보일 수 있는 변수를 나누어 캡슐화

* 클래스를 이용하여 상속과 다양성이 일어날 수 있음

* 이런 모든 것이 일어나는 언어를 객체 지향 언어라고 한다.

* 사물과 물체를 class(object)로 정의해서 프로그래밍 하는 것이 편하고 유연하게 할 수 있다.



## class와 object

* class
  * 붕어빵 틀과 같다.

> **template**
>
> **declare once**
>
> **no data in**

<br>

* object
  * 붕어빵과 같다

> **instance of a class**
>
> **created many times**
>
> **data in**

<br>

**class를 이용해서 새로운 instance를 생성하면 object가 된다. object는 클래스를 이용해서 많이 만들 수 있다. class는 정의만 한 것이므로 메모리에 올라가지 않지만, 실제로 데이터를 넣으면 object가 메모리에 올라가는 것이다. (붕어빵 틀 -> 팥붕어빵, 크림붕어빵)**



## JavaScript의 class, object

* class: template
* object: instance of a class
* JavaScript에서 class는 ES6부터 도입
  * 그 이전에는 바로 object를 만들었음
  * 기존의 prototype을 베이스로 간편하게 사용할 수 있도록 문법만 추가된 것(**syntactical sugar**)



## Class 선언과 object 생성

### Class 선언

* constructor: object를 만들 때 필요한 데이터를 전달

* method: class안에 함수를 정의

```JavaScript
class person {
// constructor
constructor(name, age){
// filed
this.name = name;
this.age = age;
}
// method
speak() {
console.log(`${this.name}: hello!`);
}
}
```

<br>

### object 생성

* new 키워드를 사용하여 생성

  * constructor의 parameter를 전달
  * 생성된 object에서 class에 정의한 method 접근 가능

```JavaScript
class Person {
// constructor
constructor(name, age){
  // filed
  this.name = name;
  this.age = age;
}
// method
speak() {
  console.log(`${this.name}: hello!`);
}
}

const myPet = new Person('siru', 4);
console.log(myPet.name); // siru
console.log(myPet.age); // 4
myPet.speak(); // siru: hello!
```



###  Getter와 Setters

```JavaScript
class User {
  constructor(firstName, lastName, age){
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
  }
}

const user1 = new User('Steve', 'Job', -1);
console.log(user1.age);
```

* 위처럼 객체 지향의 관점에서, user1의 나이가 -1이 되는 것은 말이 안된다.

<br>

* get이라는 키워드로 값을 return
* set이라는 키워드로 값을 setting

```JavaScript
class User {
  constructor(firstName, lastName, age){
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
  }
  
  // getter
  get age() {
    return this._age;
  }
  
  // setter
  set age(value) {
    if (value < 0){
      // 잘못된 값 방지, 삼항 연산자로도 방지 가능
      throw Error('age can not be negative');
    }
    this._age = value;
  }
}

const user1 = new User('Steve', 'Job', -1) // 오류 발생
console.log(user1.age);
```

age getter를 정의하는 순간, `this.age`는 메모리의 데이터를 읽어오는 것이 아니라 getter를 호출하게 된다. 그리고 setter를 정의하는 순간, `this.age = age;`에서 값을 할당할 때 setter를 호출하게 된다. 즉, setter 안에서 전달된 value를 `this.age`에 할당하는게 아니라 또 다시 setter를 호출하게 된다. 그 결과, **setter는 무한히 반복되어 call stack 이 넘치게 된다.** 

이를 방지하기 위해서 getter와 setter 안에 사용되는 변수 명을 다르게 해야한다. filed는 `_age`이지만, `.age`에 값을 할당할 수 있는 이유 내부적으로 getter와 setter가 있기 때문이다.



### Publice & Private

* 최근에 추가된 개념
  * 브라우저에서 지원하지 않는 경우가 있음
  * 사용하기 위해, babel을 사용
* 생성자를 사용하지 않고 filed를 정의 가능
* 바로 정의하면 public, #를 붙이면 private
  * private은 class 내부에서만 값이 보여지고 접근, 변경이 가능

```JavaScript
class Experiment {
  publicField = 2;
	#privateField = 0;
}

const experiment = new Experiment();
console.log(experiment.publicFiled); // 2
console.log(experiment.privateField); // undefined
```



### Static

* 최근에 추가된 개념
* object에 상관없이 class가 가지고 있는 고유한 값과 메소드를 다룰 수 있음
* Object에 상관없이 접근할 수 있어서 메모리의 사용을 줄일 수 있다.
* class 자체에서 접근할 수 있다.

```JavaScript
class Article {
  static publisher = 'siru';
	constructor (articleNumber) {
    this.articleNumber = articleNumber;
  }

	static printPublisher() {
    console.log(Article.publisher);
  }
}

const article1 = new Article(1);
const article2 = new Article(2);
console.log(article1.publisher); // undefined
console.log(Article.publisher); // siru
Article.printPublisher(); // siru
```



## 상속 & 다양성

* extends: 한 class를 또 다른 class로 확장할 수 있다.
* over riding
  * 다양성
  * 필요한 메소드를 재정의
* super: 부모의 메소드를 가져올 수 있다.

```JavaScript
class Shape {
  constructor (width, height, color){
    // filed
    this.width = width;
    this.height = height;
    this.color = color;
  }
  
  // method
  draw() {
    console.log(`drawing ${this.color} color!`);
  }
  
  getArea() {
    return width * this.height;
  }
}

// Shape의 모든것이 Rectangle에 포함된다.
class Rectangle extends Shape {}
class Tirangle extends Shape {
    draw() {
    super.draw();
    console.log(`drawing ${this.color} color!`);
  }
  getArea() {
    return (width * this.height) / 2;
  }
}

const rectangle = new Rectangle(20, 20, 'blue');
rectangle.draw();
console.log(rectangle.getArea());
const triangle = new Triangle(20, 20, 'red');
triangle.draw();
console.log(triangle.getArea());
```



## instanceOf

> **object instanceOf class;**

* 왼쪽의 object가 오른쪽의 class의 instance인지 boolean으로 return
* 상속의 관계에서도 true
* JavaScript에서, 모든 object는 Object를 상속
  * 어떤 object라도 공통적으로 존재하는 메소드 접근 가능(over riding 가능)



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)

