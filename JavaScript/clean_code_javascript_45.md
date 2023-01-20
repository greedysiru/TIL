# 클린코드 자바스크립트 - 함수 다루기(복잡한 인자 관리하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 복잡한 인자 관리하기



### 함수의 맥락 유추

* 정의된 파라미터를 보고도 함수의 맥락을 유추할 수 있게하는 것이 중요

```JavaScript
function toggleDisplay(isToggle) {
  // ...
}

function sum(number1, number2) {
  // ...
}

function genRandomNumber(min, max) {
  // ...
} 

function timer(start, stop, end) {
  // ...
}

function genSqure(top, right, bottom, left) {
  // ...
}
```



### 복잡한 인자 관리하기

* 복잡한 인자는 객체로 관리하기
  * 구조분해를 응용
  * 인자를 넘길 때 순서를 지키지 않아도 됨

```JavaScript
function createCar(name, barnd, color, type) {
  // ...
}

// 복잡한 인자들을 객체로 리팩토링
function createCar({name, brand, color, type}) {
  // ...
}

 // 명시적으로 중요한 인자는 따로 빼도 됨
function createCar(name, {brand, color, type}) {
  // 중요한 인자가 넘어오지 않았을 때의 에러처리
  if (!name) {
    throw new Error('name is a required');
  }
  // ...
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

