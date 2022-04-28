# 28장. Number(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 28.3 Number 메서드

### 28.3.1 Number.isFinite

* 정적 메서드
* 유한수인지 검사하여 불리언으로 반환



### 28.3.2 Number.isInteger

* 정적 메서드
* 정수인지 검사하여 불리언으로 반환



### 28.3.3 Number.isNaN

* ES6 정적 메서드
* NaN인지 검사하여 불리언으로 반환



### 28.3.4 Number.isSafeInteger

* 인수로 전달한 숫자값이 안전한 정수인지 검사하여 불리언으로 반환



### 28.3.5 Number.prototype.toExponential

* 프로토타입 메서드
* 전달 받은 인수를 지수 표기법 문자열로 반환
* 숫자 리터럴과 사용시 괄호를 쓸 것
  * .의 구분이 모호, 소수 구분 기호일 수도 있고 프로퍼티 접근 연산자일 수도 있기 때문



### 28.3.6 Number.prototype.toFixed

* 숫자를 반올림하여 문자열로 반환



### 28.3.7 Number.prototype.toPrecision

* 인수로 전달 받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환



### 28.3.8 Number.prototype.toString

* 숫자를 문자열로 변환하여 반환
* 진법을 나타내는 정수값을 인수로 전달 가능
  * 기본값은 10진법