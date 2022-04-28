# 20장 strict mode

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 20.1 strict mode란?

### 20.1.1 암묵적 전역

* 함수 스코프에 선언이 되지 않은 변수를 참조하더라도, ReferenceError가 발생하는 것이 아니라 전역 객체에 프로퍼티를 생성함
* 생성된 전역 프로퍼티는 전역 변수처럼 사용할 수 있게 됨

```JavaScript
function myCat() {
	cat = siru;
}
myCat();

console.log(cat);
```



### 201.1.2 strict mode

* 오타나 문법 지식의 미비로 인한 실수 방지
  * 잠재적인 오류를 발생시키기 어려운 환경 조성해야 함
* strict mode(엄격 모드)
  * ES5
  * JavaScript 언어의 문법을 좀 더 엄격하게 적영
* ESLint로도 유사한 효과를 얻을 수 있음
  * 정적 분석 기능
  * 문법적 오류와 잠재적 오류까지 찾아냄
  * 코딩 컨벤션을 설정 파일 형태로 정의, 강제 가능



## 20.2 strict mode의 적용

* 전역의 선두 또는 함수의 선두에 'use strict'; 를 추가
  * 전역에 추가하는경우 스크립트 전체에 적용 됨
  * 함수의 몸체 선두에 추가하는 경우 해당 함수의 중첩 함수에 적용 됨

```JavaScript
'use strict';

function myCat() {
	cat = siru; // ReferenceError
}
myCat();

console.log(cat);
```

