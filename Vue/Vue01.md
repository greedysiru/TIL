# Vue.js - 개발환경 설정, Vue.js 소개

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. 개발 환경 설정

### 필요 프로그램

* Chrome
* Visual Studio Code(VSC)
* Node.js



### VSC Extention

* Vetur



### Chrome Extention

* Vue.js devtools
* Live Server



## 2. Vue.js 소개

### Vue는 무엇인가?

* MVVM 패턴의 뷰모델(ViewModel) 레이어에 해당하는 화면(View)단 라이브러리

![img](https://v1.vuejs.org/images/mvvm.png)

* View: 브라우저에서 사용자에게 보여지는 화면
  * 입력박스, 버튼과 같은 HTML 요소
  * DOM: JavaScript로 조작할 수 있는 객체
* DOM Listieners: View에서 사용자가 클릭, 키보드 입력 등을 하였을 때의 이벤트를 청취
  * JavaScript의 데이터(Model)를 바꾼다.
* Data Bindings: JavaScript의 데이터(Model)이 바뀌었을 때 바로 화면에 반영



### 기존 웹 개발 방식(HTML, JavaScript)

* 데이터가 갱신되었을 때 반영을 하기 위해서 재할당을 해야했음

```JavaScript
var div = document.querySelector('#app');
var str = "Hello World";
div.innerHTML = str;
str = "hello World!";
div.innerHTML = str;
```



### Reactivity

* Vue의 핵심
* 데이터의 변화를 라이브러리에서 감지해서 화면에 자동 반영
* 데이터 바인딩
  * Object.definePropoerty: 객체의 동작을 재정의하는 API

  ```JavaScript
  var div = document.querySelector('#app');
  var viewModel = {};    
  Object.defineProperty(viewModel, 'str', {
      // 속성의 접근했을 때의 동작을 정의
      get: function () {
        console.log('접근');
      },
      // 속성에 값을 할당했을 때의 동작을 정의
      set: function (newValue) {
        console.log('할당', newValue);
        div.innerHTML = newValue;
      }
  });
  ```



### Reactivity 코드 라이브러리화 하기

* 각 기능별로 함수화
* 즉시 실행 함수 안에 넣기
* 즉시 실행 함수 표현(IIFE, Immediately Invoked Function Expression)
  * 정의되자마자 즉시 실행되는 함수
  * 전역 스코프에 불필요한 변수를 추가해서 오염시키는 것을 방지
  * IIFE 내부안으로 다른 변수들이 접근하는 것을 막을 수 있음

```JavaScript

    // 즉시 실행 함수
    (function () {
      function init() {
        Object.defineProperty(viewModel, 'str', {
          // 속성의 접근했을 때의 동작을 정의
          get: function () {
            console.log('접근');
          },
          // 속성에 값을 할당했을 때의 동작을 정의
          set: function (newValue) {
            console.log('할당', newValue);
            // 새 값을 할당
            render(newValue);
          }
        });
      }
      // div의 텍스트 값을 할당하는 함수
      function render(value) {
        div.innerHTML = value;
      }

      init();
      
    })();
```

# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

[Vue 이미지](https://v1.vuejs.org/images/mvvm.png)

