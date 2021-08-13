# Webpack - 웹팩이 필요한 이유와 모듈 시스템



**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 웹팩이 필요한 이유

* 전역 스코프의 오염 위험
  * 예) 전역 스코프에 함수나 변수를 선언하면 다른 파일에서도 접근이 가능
  * 애플리케이션이 예측할 수 없게 되고 런타임 에러가 발생



## 2. IIFE 방식의 모듈

* 즉시 실행 함수 표현(IIFE, Immediately Invoked Function Expression)
* 전역 스코프 오염 문제를 예방하기 위해 사용
* 함수 외부에서 함수 내부를 접근할 수 없음
  * 외부로부터 독립적

```JavaScript
var math = math || {};

(function() {
  // 함수 안에 넣음으로써 독립적
  function sum(a, b) {
    return a + b;
  }
  
  // math에 할당함으로 외부에서 사용할 수 있음
  math.sum = sum;
  
}());
```



## 3. 다양한 모듈 시스템

* 자바스크립트 모듈을 구현하는 대표적인 명세: AMD, CommonJS
* CommonJS
  * JavaScript를 사용하는 모든 환경에서 모듈을 하는 것이 목표
  * exports 키워드로 모듈을 생성
  * require 함수로 모듈을 불러들임
  * Node.js에서 사용
*  AMD(Asynchronous Module Definition)
  * 비동기로 로딩되는 환경에서 모듈을 사용하는 것이 목표
  * 주로 브라우저 환경
* UMD(Universal Module Definition)
  * AMD기반으로 CommonJS 방식 지원
* ES2015 표준 모듈 시스템
  * 현재 Webpakc, Babel로 일반적으로 사용하는 모듈 시스템
  * export 구문으로 모듈 생성
  * import 구문으로 모듈 불러들임



## 4. 브라우져의 모듈 지원

* 인터넷 익스플로러와 같은 몇 몇 브라우져는 모듈을 지원하지 않음 
* Webpack을 사용하면, 브라우져에 무관하게 모듈을 사용가능하다.

# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)