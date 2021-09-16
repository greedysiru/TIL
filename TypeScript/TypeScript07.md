# 타입스크립트 입문 - 이넘, 클래스

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 이넘

### 이넘이란

* 특정 값들의 집합을 의미하는 자료형
* dropdown과 같은 정해진 목록을 사용할 때 유용



### 숫자형 이넘

* 이넘에 별도의 값을 지정하지 않고 선언하면 기본적으로 숫자형 이넘
* 초기 값을 주면 초기 값부터 차례로 1씩 증가
* 초기 값을 주지 않으면 0부터 차례로 1씩 증가

```TypeScript
enum Shoes {
  Nike,
  Adidas,
  NewBalnce
}
// 별도의 값을 지정하지 않으면 숫자형 enum으로 지정
let myShoes = Shoes.NewBalnce;

console.log(myShoes); // 2 enum member
```



### 문자형 이넘

* 특정 문자 또는 또 다른 이넘 값으로 초기화해야 함

```TypeScript
enum Shoes {
  Nike = "나이키",
  Adidas = "아디다스",
  NewBalnce = "뉴발란스"
}
// 별도의 값을 지정하지 않으면 숫자형 enum으로 지정
let myShoes = Shoes.NewBalnce;

console.log(myShoes); // 뉴발란스
```

* 위 코드의 실제 동작 코드

```JavaScript
"use strict";
var Shoes;
(function (Shoes) {
    Shoes["Nike"] = "\uB098\uC774\uD0A4";
    Shoes["Adidas"] = "\uC544\uB514\uB2E4\uC2A4";
    Shoes["NewBalnce"] = "\uB274\uBC1C\uB780\uC2A4";
})(Shoes || (Shoes = {}));
let myShoes = Shoes.NewBalnce;
console.log(myShoes);
```



### 이넘 활용

* 정해진 값만 사용되도록 할 수 있다.
  * 이넘에서 정의된 데이터만 사용
* 정확한 코드를 사용할 수 있음
* 예외 처리를 줄일 수 있음

```TypeScript
enum Answer {
  Yes = 'Y',
  No = 'N',
}

// answer 파라미터는 Answer 이넘에 정의된 것만 사용 가능
function askQuestion(answer: Answer) {
  if (answer === Answer.Yes) {
    console.log('정답입니다');
  }
  if (answer === Answer.No) {
    console.log('오답입니다');
  }
}

// 파라미터로 함수 선언부에 정의된 이넘만 사용 가능
askQuestion(Answer.Yes);

// 아래의 함수 사용은 이넘을 사용하지 않았으므로 오류 발생
askQuestion('yes');

askQuestion('y');

askQuestion('Yes');

askQuestion('예스');
```



## 2. 클래스

### 클래스란

* ES2015(ES6) 부터 지원
* constructor: 초기화 메소드

```JavaScript
class Person {
  constructor(name, age) {
    console.log('생성 되었습니다');
    this.name = name;
    this.age = age;
  }
}

let greedySiru = new Person('siru', 6); // 생성 되었습니다.
console.log(greedySiru);
```



### 자바스크립트 프로토타입

* 자바스크립트는 프로토타입 기반의 언어
* 프로토타입으로 상속을 사용할 수 있다.
* 모든 타입은 프로토타입을 가진다.

```JavaScript
let user = { name: 'siru', age: 6};

// 빈 객체
let admin = {};

// 상속
// admin의 프로토타입에 user를 정의
// user의 정보를 물려 받음
admin.__proto__ = user;
admin.name; // 'siru'
```



### 프로토타입의 활용 사례

* 타입마다의 메소드는 프로토타입으로부터 상속 받은 것
  * Built-in JavaScript API 또는 JavaScript Native API라고 부름

```JavaScript
let obj = { a: 10 };

Object.keys(obj); // ["a"]
```



### 프로토타입과 클래스의 관계

* 자바스크립트의 class는 문법적 설탕임
  * 기존에 이미 제공되어 왔음(생성자 함수)

```JavaScript
function Person(name, age) {
  this.name = name;
  this.age = age;
}
```



### 타입스크립트의 클래스 문법

* 클래스의 최상단에 클래스가 사용할 멤버 변수의 타입을 정의
* private: 클래스 안에서만 접근 가능
* public: 클래스 밖에서도 접근 가능
* readonly: 접근만 가능하고 값을 변경 불가

```TypeScript
class Person {
  private name: string;
  public age: number;
  readonly log: string;

  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```



# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)