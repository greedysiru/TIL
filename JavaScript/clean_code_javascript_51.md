# 클린코드 자바스크립트 - 함수 다루기(순수 함수)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 순수 함수

* JavaScript는 동적인 언어
  * this, scope, 실행 컨텍스트 등
* JavaScript는 주로 브라우저에서 실행 됨
  * 사용자의 입력을 제어하기 어려움



### Redux의 예

* 자바스크립트 앱을 위한 예측 가능한 상태 컨테이너
* **순수 함수를 사용**
  * 함수에서 side effect를 일으키면 안 됨
* side effect
  * logging
  * saving
  * setting async timer
  * Making an AJAX HTTP Request
  * 함수 외부의 상태를 변경
  * 난수를 생성



### 순수 함수가 아닌 예

* 함수의 결과가 예측이 안 됨

```JavaScript
let num1 = 10;
let num2 = 20;

// 아래 두 함수는 외부 상태를 참조
function impureSum() {
  return num1 + num2;
}

impureSum(); // 30
// 외부 상태가 바뀌면 함수의 결과도 달라짐
num1 = 30;
impureSum(); // 50
```



### 순수함수의 예

* 함수의 결과가 예측이 가능

```JavaScript
function pureSum(num1, num2) {
 	return num1 + num2; 
}

pureSum(10, 20); // 30
```



### 참조형 자료형의 경우

* 객체를 전달받아 함수 내부에서 변경하더라도 원본이 변경됨에 주의할 것
* 전달 받은 객체를 복사하고 조작한 뒤 새로운 객체를 return하기

```JavaScript
// 참조형 자료형(객체)의 경우
const obj = { one: 1 };

function changeObj(targetObj) {
  targetObj.one = 100;
  
  return targetObj;
}

changeObj(obj); // { one: 100 }
// 함수 외부의 객체인 obj 원본 또한 바뀜
console.log(obj) // { one: 100 }

// 전달받은 객체를 복사하기
function changeObj(targetObj) {
  return {...targetObj, one: 100};
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

