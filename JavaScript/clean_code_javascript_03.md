# 클린코드 자바스크립트 - 변수(전역 공간 사용 최소화)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. window vs. global

* 둘 다 최상위 공간을 의미(전역 공간)
* window: **브라우저**에서의 전역 공간
  * web api 명세가 존재
  * setTimeout, setInterval, alert
* global: **Node.js**에서의 전역 공간
* 둘의 큰 차이는 없음



## 2. 전역 공간 오염

* var로 선언한 변수는 window 객체 안에 할당 됨(전역 공간)
* 전역 공간에 선언된 경우, 다른 js 파일에서도 접근 가능
* web api와 같은 식별자로 할당하는 경우, 덮어쓰기가 되어버림
* **전역 공간은 어디서나 접근이 됨**
  * 지역변수를 사용할 것
  * window, global에 접근하여 조작하지 말기
  * let & const 키워드를 사용하기
  * IIFE, module, closure를 사용하여 스코프를 나누기



### index.html

```html
...
<script src='./index.js'></script>
<script src='./index2.js'></script>
</body>
```



### index.js, index2.js

```JavaScript
// index.js
var ex = '예시';
var setInterval = '덮어쓰기';
```



```JavaScript
// index2.js
console.log(ex); // 예시
console.log(window.ex); // 예시
console.log(setInterval); // 덮어쓰기
console.log(window,setInterval); // 덮어쓰기
```



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

