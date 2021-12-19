# JavaScript - this

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. JavaScript의 변수 scope

* JavaScript의 변수 scope는 기본적으로 전역임
  * JavaScript 변수를 선언하면, window(브라우저 객체)에 생성됨



## 2. window 객체

* 브라우저 객체
* 브라우저에 대한 정보, DOM에 대한 접근을 나타냄
* 모든 변수, 함수의 최상단에 있음
* **첫번째 this는 window 객체를 가리킴**

```JavaScript
consoel.log(this); // window
```





## 3. function 선언문

* 함수 안에서의 **this 또한 window**를 가리킴
  * **두번째 this**
* 이와같은 혼동을 방지하기 위해서 **'use strict'(strict mode) 사용**

```JavaScript
function callThis() {
  console.log(this);
}

callThis(); // window
```



## 4. 생성자 함수

* 생성자 함수의 **this는 인스턴스 자체를 정의한 객체(생성자 함수)**를 가리킴
  * **세번째 this**

```JavaScript
function Vue(el) {
  console.log(this);
  this.el = el;
}

new Vue('#app'); // Vue {}
```



## 5. 비동기 처리

* 비동기 처리 안에서의 **this는 undefined**
  * 네번째 this
* 호출되는 시점에서 새로운 this가 생김
* 그러므로, 함수 선언식같은 경우에는 this 바인딩을 해야함



```JavaScript
// 비동기 함수, Promise를 return
fetchNewsList()
	.then(function(response) {
  	console.log(this); // undefined
})
	.catch(function(error) {
    console.log(error);
});


```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

