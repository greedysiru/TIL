# ES6 - Arrow Function

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## Arrow Function - 화살표 함수

* 함수를 정의할 때 **function**이라는 키워드를 사용하지 않고 **=>**로 대체
* **콜백 함수**의 문법을 간결화



### 사용 문법

```JavaScript
// ES5 함수 정의 방식
const sumA = function(a, b) {
  return a + b;
};

// ES6 함수 정의 방식
const sumB = (a, b) => {
  return a + b;
}
```



### 사용 예시

* 콜백을 사용할 때 더 간결한 문법으로 사용할 수 있음
* 가독성과 웹페이지의 바이트수 를 줄일 수 있음

```JavaScript
// ES5
const arrA = ['a', 'b', 'c'];
arrA.forEach(function(value) {
  console.log(value); // a, b, c
});

// ES6
const arrB = ['a', 'b', 'c'];
arrB.forEach(value => console.log(value)); // a, b, c
```



# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

