# ES6 - Modules

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## Modules - 자바스크립트 모듈화 방법

* ES5 이전에는 모듈화 방법이 없었음
  * AMD, Commons JS 를 사용
* 모듈: 특정 기능을 수행하는 한 묶음
  * 재사용성이 뛰어난 기능을 한데 묶음
* 자바스크립트 모듈 로더 라이브러리(AMD, Commons JS) 기능을 js 언어 자체에서 지원
  * 파일별로 스코프를 가지게 됨
* 호출되기 전까지는 코드 실행과 동작을 하지 않는 특성

```JavaScript
// libs/math.js
export function sum(x, y) {
  return x + y;
}
export const pi = 3.141593;

// main.js
import {sum} from 'libs/math.js';
sum(1, 2); // 3
```



## default export

* **default**: 한 개 파일에서 하나만 export
* import 할 때 원하는 이름으로 가져올 수 있음

```JavaScript
// util.js
export default function (x) {
  return console.log(x);
}

// main.js
import util from 'util.js';
console.log(tuil); // function (x) { return console.log(x) };

// app.js
import log from 'util.js';
console.log(log); // function (x) { return console.log(x) };
```



# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

