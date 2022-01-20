# Vue.js -  UX를 고려한 데이터 호출 시점

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 데이터 호출 시점

* 컴포넌트 라이프 사이클 훅
  * created : 컴포넌트가 생성되지마자 실행되는 로직
* 라우터 네비게이션 가드
  * 뷰 라우터로 특정 URL에 접근 시, 해당 URL의 접근을 막는 방법
* **라우터 네비게이션 가드가 컴포넌트 라이프 사이클 훅보다 선행**



## 2. 컴포넌트 라이프 사이클 훅

### 라이프 사이클

* beforeCreate
  * 인스턴스가 방금 초기화 된 후 호출
* created
  * 인스턴스(컴포넌트)가 작성된 후 호출
  * **데이터 처리, 계산된 속성, 메서드, 감시/이벤트 콜백 등과 같은 옵션 처리를 완료**
  * **API 호출 시점**
* beforeMount
  * 마운트가 시작되기 바로 전에 호출
* mounted
* beforeUpdate
  * 데이터가 변경 시, 가상 DOM 재 레넏링과 패치가 이뤄지기 전에 호출
* updated
  * 데이터가 변경되어 가상 DOM이 재 렌더링되고 패치되면 호출
* activated
* deactivated
* destroyed
* errorCaptured



## 3. 네비게이션 가드

* vue-rotuer에서 제공하는 기능
* 특정 URL 접근 시 리다이렉팅 또는 취소하는 것에 사용
* 이 시점에 데이터 호출을 하는 것이 가능

# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

