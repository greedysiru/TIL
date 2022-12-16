# 클린코드 자바스크립트 - 타입 다루기(isNaN)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. IEEE 754

* 컴퓨터에서는 수를 이진수로 다룸
  * 이로인해 컴퓨터에서는 소수점을 다루는 것이 까다로움
* JavaScript에서는 IEEE 754(부동소수점 방식)을 사용하여 소수점을 다룸
  * 부동: 떠돌이



## 2. Number

* 숫자를 표현하고 다룰 때 사용하는 원시 래퍼 객체



### MAX_SAFE_INTEGER

* JavaScript가 최대로 다룰 수 있는 안전한 수(원시 객체가 가지고 있는 property)



### isInteger()

* 주어진 값이 정수인지 확인하여 boolean을 return하는 method



### isNaN()

* NaN: is Not A Number
  * 숫자가 아님을 표현하는 자료형
* 주어진 값이 NaN인지 확인하여 boolean을 return하는 method
* NaN 자체에 부정이 내포되어 있어 혼동에 주의
* ECMAScript 2015에서 추가 됨



## 3. isNaN()

* 어떤 값이 NaN인지 판별하는 빌트인 함수
* 느슨한 검사를 함에 주의
  * false이면 숫자가 맞다는 뜻




### vs Number.isNaN()

* 엄격한 검사를 함
  * 주어진 값이 NaN인지 아닌지를 엄격하게 확인

* `Number.isNaN()`을 사용하는 것을 권장
* 아래와 같은 동작을 함

```JavaScript
isNaN = function(value) {
    Number.isNaN(Number(value));
}
```



### isNaN의 혼란스러운 케이스

```JavaScript
isNaN(111 + 'test'); // true
// + 연산자로인해 '111test'로 평가 -> string이므로  flase이어야 함

Number.isNaN(111 + 'test'); // false
// 엄격한 검사를 하여, string이므로 false return
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

[[MDN] isNaN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/isNaN)