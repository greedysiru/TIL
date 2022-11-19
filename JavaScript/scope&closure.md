# 기초 JS, CS 상식 - 스코프와 클로저



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 1. 스코프

* 유효 범위
* 변수가 어느 범위까지 참조되는 지를 뜻함
* 전역 스코프(Global Scope): 어디서든 접근 가능
* 지역 스코프(Local Scope): 해당 스코프 내에서만 접근 가능



### var

* 예기치 못한 오류가 생길 수 있음
* 호이스팅되어 변수 선언이 함수 상단으로 올라가 버림
* 함수 수준의 스코프를 가짐
* 블록 내부에 새롭게 선언하더라도 블록 외부 변수값도 같이 변하게 됨
* **변수 선언 시, var 키워드는 지양**



## 2. 클로저

* 함수가 선언된 스코프를 기억하여 함수가 스코프 밖에서 실행되어도 기억한 스코프에 접근할 수 있게 만드는 문법
* 닫힘, 폐쇄
* 외부에서 접근이 불가능한 영역을 클로저를 통해서만 접근 가능
* 은닉화
  * 내부 변수와 함수를 숨길 수 있음



### 예시1

```JavaScript
function example() {
  // example 함수 내 지역 스코프
  // 본래 함수가 종료되면 메모리에서 사라짐
  const inner = '내부 변수';
  
  // 반환된 함수가 inner를 참조
  // 해당 변수는 메모리에서 사라지지 않음
  return function() {
    console.log(inner);
  }
}

const closure = example();

closure(); // '내부 변수'가 출력
```



### 예시2

* 클로저로 인해 예기치 못한 상황이 발생할 수 있음

```JavaScript
function timeoutCounting() {
  let i = 0;
  for (i = 0; i < 5; i+= 1){
    setTimeout(function () {
      console.log(i);
    }, i * 100);
  }
}

timeoutCounting(); // 5 5 5 5 5

// 1 2 3 4 5가 아닌, 5만 다섯번이나옴
// closure가 원인
// setTimeout의 대기시간이 끝나 콜백함수가 실행되는 시점에는 루프가 종료되어 i가 5가되었기 때문
```



### 3. 클로저 해결 방법

* 상기, 클로저로 인해 예기치 못한 현상이 발생할 수 있음



### IIFE

* IIFE(Immediately Invoked Function Expression)
* 즉시 실행 함수

```JavaScript
function counting() {
  let i = 0;
  for (i = 0; i < 5; i+= 1){
    // 즉시 실행 함수로 인해 각 루프마다 closure가 생성됨
    (function (number) {
      setTimeout(function () {
	      console.log(number);
    	}, number * 100);
    })(i);
  }
}

counting(); // 0 1 2 3 4
```



### let

* 블록 수준의 스코프기 때문에 매 루프마다 클로저가 생성

```JavaScript
function counting() {
  for (let i = 0; i < 5; i+= 1){
      setTimeout(function () {
	      console.log(number);
    	}, number * 100);
  }
}

counting(); // 0 1 2 3 4
```





## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

