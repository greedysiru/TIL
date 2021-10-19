# ES6 - const & let

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. const & let

* **블록 단위**로 변수의 범위가 제한
  * 블록단위란, { }를 말함
* const: 한 번 선언한 값에 대해서 변경할 수 없음 (상수 개념)
  * 재할당 불가능
* let: 한 번 선언한 값에 대해서 다시 선언할 수 없음
  * 재할당 가능
  * 재선언 불가능



### ES6 - 블록 스코프

* 블록 단위로 변수의 범위가 제한

```JavaScript
let sum = 0;
for (let i = 1; i <= 5; i++) {
  sum = sum + i;
}

console.log(sum); // 10
console.log(i); // i 접근 불가
```



### ES6 - const(상수)

* 선언 후 할당한 값은 변경 불가능

```JavaScript
const a = 10;
a = 5; // Error
```

* 단, 참조형인 객체, 배열의 내부는 변경할 수 있다.

```JavaScript
const a = {};
a.num = 10;
consoel.log(a); // {num: 10}

const b = [];
b.push(20);
console.log(b); // [20]
```



### ES6 - let(변수)

* 선언한 값에 대해서 다시 선언 불가

```JavaScript
let b = 10;
let b = 20; // Error
```



## 2. 변수 스코프와 호이스팅

### ES5 특징 - 변수의 Scope

* 기존 자바스크립트(ES5)는 블록에 상관 없이 스코프가 설정됨

```JavaScript
var sum = 0;
for (var i = 1; 1 <= 5; i++) {
  sum = sum + 1;
}
console.log(sum); // 15
console.log(i); // 6, 블록을 벗어나도 i에 접근이 됨
```



### ES5 특징  - Hoisting

* Hoisiting이란 선언한 함수와 변수를 해석기가 가장 상단에 있는 것처럼 인식
* js해석기는 코드의 라인 순서와 관계 없이 함수 선언식과 변수를 위한 메모리 공간을 먼저 확보
* 함수 선언식과 var는 코드의 최상단으로 끌어 올려진 것처럼 동작
  * 함수 선언식: **function 함수명() {}**
  * 함수 표현식: **const 함수명 = function () {}**

```JavaScript
function hoistedFunction() {
  return 10;
}
hoistedFunction(); // 5
function hoistedFunction() {
  return 5;
}
```



## 3. const & let 심화 예시

```JavaScript
function f() {
  {
    let x;
    {
      // 새로운 블록 안에서 x를 상수로 선언 가능
      const x = 'hi';
      // const이므로 재할당불가
      x = 'hello';
    }
    // 같은 블록의 let x에 할당 가능
    x = 'hoho';
    // 같은 블록에서 이미 let x가 선언되어 있으므로 재선언 불가
    let x = 'bye';
  }
}
```



# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

