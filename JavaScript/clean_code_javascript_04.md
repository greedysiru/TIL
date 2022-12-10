# 클린코드 자바스크립트 - 변수(임시변수 제거하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 임시변수란

*  특정 공간 scope 안에서 전역 변수처럼 사용되는 변수
*  함수가 커졌을 때, 임시 변수를 작성하는 습관이 있다면 전역 변수처럼 문제를 일으킬 수 있음



### 예시 코드

```JavaScript
function getElements() {
  // getElements 함수의 임시 객체
  const elements = {};
  
  // DOM API를 통해 Element들을 임시 객체에 넣음
  elements.title = document.querySelector('.title');
  elements.text = documents.querySelector('.text');
	elements.value =  documents.querySelector('.value');
  
  return elements;
}
```



## 2. 임시 객체 제거

* 위의 예시 코드 임시 객체를 아래와 같이 정리할 수 있음
* 객체 생성, 점표기법으로 접근하여 할당하는 위의 것보다 side effects를 줄일 수 있음
  * 임시 객체를 만들지 않아 접근할 일이 없기 때문



### 예시 코드

```JavaScript
function getElements() {
  return {
    title: documents.querySelector('.title'),
    text: documents.querySelector('.text'),
    value: documents.querySelector('.value'),
  };
}
```



## 3. 임시 변수를 제거해야 하는 이유

* 함수를 정의할 때, 단 하나의 역할만 하도록 정의해야 함
  * return하는 값이 무엇인지 예측이 되어야 함
* 임시 변수를 선언하고 crud와 같은 조작을 많이 하면, 명령으로 가득한 로직이 되어 버림
  * 디버깅이 어려워 짐
  * 접근, 할당 로직을 추가가 될 우려가 있음
  * 유지보수가 어려워 짐



### 임시 변수를 제거하는 방법

* 함수를 최대한 나누고 예측 가능한 값을 return
* 고차함수 활용(map, filter, reduce)
* 선언형 프로그래밍 지향



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

