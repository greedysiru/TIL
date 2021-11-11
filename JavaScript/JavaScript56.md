# ES6 Modules 문법

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. import & export 기본 문법

* 모듈화 기능을 사용



### export

* 다른 파일에서 가져다 사용할 변수, 함수 앞에 export 키워드 붙임
* export된 파일은 import로 불러와 사용 가능

```javascript
export 변수, 함수
```



### import

* export된 함수 또는 변수를 {}에 선언
* 파일 경로는 상대 경로

```JavaScript
import { 불러올 변수 또는 함수 이름 } from '파일경로';
```



## 2. import & export 예시

```javascript
// math.js
export function sum(a, b) {
  return a + b;
}

// app.js
import { sum } from './math.js';
conosle.log(sum(10, 20)); // 30
```



# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)

