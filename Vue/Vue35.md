# Vue.js - v-html, router transition

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. v-html

* 문자열에 포함된 태그 정보를 인식하여 태그로 변환
* element의 innerHTML을 업데이트
* XSS 공격으로 이루어질 수 있으므로 매우 위험할 수도 있음
  * 신뢰할 수 있는 컨텐츠에만 v-html을 사용할 것

### 예시

```html
<div v-html="fetchedItem.content"></div>
```



## 2. router transition

* 특정 링크로 이동 시 Vue 내부적으로 제공되는 transition API를 사용하여 부드러운 화면 전환 구현



### 적용

```Vue
<template>
  <div id="app">
    <!-- 지정한 라우트에 따라서 컴포넌트가 나타나게 됨 -->
    <tool-bar></tool-bar>
    <!-- transition의 name page가 Vue 내부적으로 css 규칙에 prefix 됨 -->
    <transition name="page">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
import ToolBar from './components/ToolBar.vue';

export default {
  components: {
    ToolBar,
  },
}
</script>

<style>
/* Rotuer Transition */
/* enter-active, levae-active, enter, leave-to 등의 단계 앞에 page가 붙고 css가 적용 됨 */
.page-enter-active, .page-leave-active {
  transition: opacity .5s;
}
.page-enter, .page-leave-to /* .page-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>

```



### Transition Classes

* Vue에 정의된 Transition Classes
* v-enter: enter의 시작 상태
  * 엘리먼트가 삽입되기 전에 적용되고 한 프레임 후에 제거
* v-enter-active: enter에 대한 활성 및 종료 상태
  * 엘리먼트가 삽입되기 전에 적용
  * Transition / Animation이 완료되면 제거
* v-enter-to: 진입 상태의 끝에서 실행
  * 엘리먼트가 삽입된 후 (동시에 v-enter 제거 됨), Transition / Animation이 완료되면 제거
* v-leave: leave를 위한 시작 상태
  * 진출 Transition이 트리거될 때 적용되고 한 프레임 후에 제거
* v-leave-active: leave에 대한 활성 및 종료 상태
  * 진출 Transtion이 적용되고 Transition / Animation이 완료되면 제거 됨
* v-leave-to: 진출 상태의 끝에서 실행
  * 진출 Transition이 트리거되고 (동시에 v-leave가 제거됨), Transition / Animation이 끝나면 제거되는 하나의 프레임 추가

![transition](https://vuejs.org/images/transition.png)

# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

[Vue transition 공식 문서](https://vuejs.org/v2/guide/transitions.html)