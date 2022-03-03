# 17장 - 생성자 함수에 의한 객체 생성(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 17.2 생성자 함수



### 17.2.4 내부 메서드 [[Call]]과 [[Construct]]

* 함수 또한 객체
  * 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 가지고 있음
  * 일반 객체와 동일하게 동작
* 함수는 객체와 다르게 호출할 수 있음
  * 함수만이 가지고 있는 내부 슬롯과 내부 메서드를 추가로 가짐
  * [[Enviroment]], [[FormalParameters]], [[Call]], [[Construct]]
* 일반 함수로서 호출 시 ,[[Call]] 메서드 실행
  * callable
  * 모든 함수 객체는 반드시 Callable
* new 연산자화 함께 호출 시, [[Construct]]가 호출
  * constructor
  * [[Constructor]]를 가지지 않는 함수 객체는  non-constructor



### 17.2.5 constructor와 non-constructor의 구분

* 함수 정의 방식에 따라 함수를 constructor, non-constructor로 구분
* constructor : 함수 선언문, 함수 표현식, 클래스
* non-constructor : **메서드 축약 표현,** 화살표 함수
* 일반 함수로 정의된 메서드는 ECMAPScript 사양의 메서드가 아님
  * 즉, constructor



### 17.2.6 new 연산자

* new 연산자화 함수를 함께 호출하면 함수는 생성자 함수로서 동작
  * [[Constructor]]가 호출
  * 함수는 constructor이어야 함
* 생성자 함수를 new 연산자 없이 호출하면 일반 함수로서 동작
  * [[Call]]이 호출
* JavaScript에서 일반 함수와 생성자 함수의 형식적 차이는 없으므로 명명법으로 구분해야 함
  * 생성자 함수는 파스칼 케이스로 명명



### 17.2.7 new.target

* 생성자 함수가 new 연산자 없이 호출되는 것을 방지
* constructor인 모든 함수 내부에서 사용
  * 메타 프로퍼티
* new 연산자와 호출되었는지 확인 가능
  * new 연산자와 함께 호출되면, 함수 자신을 가리킴
* 대부분의 빌트인 함수는 new 연산자 없이 호출해도 new 연산자와 같이 호출했을 때와 동일하게 동작

```JavaScript
const Cat = function(name) {
  
  // 일반 함수로서 호출되면 new.target은 undefined
  // 즉 아래의 조건을 충족하여 new 연산자와 호출
  if (!new.target) {
    return new Cat(name);
  }
  
  this.name = name;
  introduce = function() {
    console.log(`My name is ${this.name}`);
  }
}
```

