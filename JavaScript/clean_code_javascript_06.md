# 클린코드 자바스크립트 - 타입 다루기(타입 검사)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. typeof 연산자

* 우항의 피연산자의 타입을 문자열로 반환
* Primitive 자료형을 분류하기 용이
* Reference(array, function, Date) 자료형은 typeof로 분류하기 어려움
  * function, class는 function으로 return
  * wrapper 객체는 object로 return
  * null은 object로 return(언어적인 오류)
* JavaScript는 동적인 언어로 타입 또한 동적임
  * 타입 검사가 어려움
  * 상황에 맞는 타입 검사를 서치를하여 활용



## 2. instanceof 연산자

* 객체의 prototype chain을 검사
* 좌항의 인스턴스가 우항의 생성자 함수로부터 만들어진 것인지 boolean으로 return
* chain의 끝(최상위)은 Object이므로 모든 Reference 자료형은 우항에 Object가 있으면 true를 return

```JavaScript
// 생성자 함수 선언
function Cat(name) {
  this.name = name;
}

const siru = new Cat('siru');

siru instanceof Cat; // true

const date = new Date();

date instanceof Date; // true

siru instanceof Object; // true
date instanceof Object; // true
```



## 3. wrapper 객체 감지하기

* 객체가 텍스트 값으로 표시되거나 객체가 문자열이 예상되는 방식으로 참조 될 때 toString 메서드를 자동 호출
  * Object에서 비롯된 모든 객체에 상속
* toString메서드가 지정 개체에서 재정의되지 않으면 [object type]을 반환

```JavaScript
Object.prototype.toString.call(new String()); // [object String]
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

[[MDN] Object.prototype.toString()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

