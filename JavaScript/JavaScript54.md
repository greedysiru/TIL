# ES6 - Enhanced Object Literals

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## Enhanced Object Literals - 향상된 객체 리터럴

* 객체의 속성을 메서드로 사용할 때 function 예약어를 생략하고 생성 가능

```JavaScript
const dictionary = {
  words: 100,
  // ES5
  lookupA: function() {
    conosle.log('find words');
  },
  // ES6
  lookupB: function() {
    console.log('find words');
  }
}
```



## 속성명의 축약

* 객체의 속성명과 값 명이 동일할 때 아래와 같이 축약 가능

```JavaScript
const figures = 10;
const dictionary = {
  figures
}
```



# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

