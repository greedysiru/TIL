# Vue.js - Vuex, Flux & MVC

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. Vuex 소개

* 무수히 많은 컴포넌트의 데이터를 관리하기 위한 상태 관리 패턴이자 라이브러리
* React의 Flux 패턴에서 기인



## 2. Flux & MVC

### Flux란?

* MVC 패턴의 복잡한 데이터 흐름 문제를 해결하는 개발 패턴 - Unidirectional data flow
  * **모든 데이터 흐름이 한 방향으로**
  * 부모 -> 자식
  * 데이터 흐름을 제한함으로, 복잡도를 낮추어 문제 발생을 방지
  * 데이터 흐름을 예측할 수 있음

> **Action -> Dispatcher -> Model -> View**

1. Action: 화면에서 발생하는 이벤트 또는 사용자의 입력
2. Dispatcher: 데이터를 변경하는 방법, 메서드
3. Model: 화면에 표시할 데이터
4. View: 사용자에게 비춰지는 화면



### MVC란?

* 데이터 처리가 많은 방향으로 일어남
  * 양방향

> **Controller -> Model <-> View**

1. Controller: Model과 View를 제어
2. Model: 데이터
3. View: 사용자에게 비춰지는 화면



### MVC 패턴의 문제점

* 기능 추가 및 변경에 따라 생기는 문제점을 예측할 수가 없음
* 앱이 복잡해지면서 생기는 업데이트 루프



## 3. Vuex

### Vuex가 필요한 이유

* 복잡한 애플리케이션에서 컴포넌트의 개수가 많아지면 컴포넌트 간에 데이터 전달이 어려워 짐
* 이벤터 버스를 사용하는 경우, 어디서 이벤트를 보냇는지 혹은 어디서 이벤트를 받았는지 알기 어려움
  * 컴포넌트 간 데이터 전달이 명시적이지 않음



### Vuex로 해결할 수 있는 문제

1. MVC 패턴에서 발생하는 구조적 오류
2. 컴포넌트 간 데이터 전달 명시
3. 여러 개의 컴포넌트에서 같은 데이터를 업데이트 할 때 동기화 문제



### Vuex 컨셉

* State: 컴포넌트 간에 공유하는 데이터
  * data( )
  * 여러 컴포넌트들이 사용하는 data 프로퍼티 같은 것
* View: 데이터를 표시하는 화면
  * template
* Action: 사용자의 입력에 따라 데이터를 변경
  * methods

> **State -> View -> Actions -> state ...**



### Vuex 구조

* 컴포넌트 -> 비동기 로직 -> 동기 로직 -> 상태
 ![vuex](https://vuex.vuejs.org/vuex.png)

# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

[Vuex](https://vuex.vuejs.org/kr/)

