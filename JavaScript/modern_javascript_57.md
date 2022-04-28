# 25장. 클래스(5)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

### 25.8.4 서브클래스의 constructor

* constructor 생략 시 비어있는 constructor가 암묵적으로 정의
* 서브클래스의 경우, 아래와 같은 constructor가 암묵적 정의

```JavaScript
constructor(...args) { super(...args); }
```



### 25.8.5 super 키워드

* 함수처럼 호출할 수 있고 this와 같이 식별자처럼 참조할 수 있는 특수 키워드



#### super 호출

* 수퍼클래스의 constructor를 호출
  * 서브클래스에서 암묵적으로 constructor를 호출하면서 super 또한 호출
* 서브클래스에서 constructor를 생략하지 않는 경우 서브클래스의 constructor에서 반드시 super 호출
* 서브클래스에서 super를 호출하기 전에는 this를 참조 불가
* super는 반드시 서브 클래스의 constructor에서만 호출
  * 이외에서 호출하면 Error 발생



#### super 참조

* 메서드 내에서 super를 참조하면 수퍼클래스의 메서드를 호출
* 자신을 참조하고 있는 메서드가 바인딩되어 있는 객체의 프로토타입을 가리킴
  * 단, call 메서드로 해당 인스턴스의 this를 전달해야 함
  * 그렇지 않으면 프로토타입의 this를 가리킴
* super 참조가 동작하기 위해서는 super를 참조하고 있는 메서드가 바인딩되어 있는 객체의 프로토타입을 찾을 수 있어야 함
  * 내부 슬롯 [[Homobject]]가 존재해야 함
  * ES6 메서드 축약 표현으로 정의된 함수만이 가짐



```JavaScript
// 수퍼클래스
class Cat {
  static say() {
    return '야옹';
  }
}

// 서브클래스
class Siru extends Cat {
  static say() {
    return `${super.say()}하고 울줄 알았냐?`;
  }
}
```

