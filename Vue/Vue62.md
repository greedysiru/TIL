# Vue.js - Vue Router, 컴포넌트 간 데이터 전달, Vuex

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. Vue Router

### 1.1 Declarative

* a태그와 같이 특정 요소를 클릭하면 지정한 경로로 이동

```Vue
<template>
  <header>
    <div>
      <router-link to="/" class="logo">
        TIL
      </router-link>
    </div>
    <div class="navigations">
      <router-link to="/login">로그인</router-link>
      <router-link to="/signup">회원가입</router-link>
    </div>
  </header>
</template>
...
```



### 1.2 Programmatic

* JavaScript 레벨에서 지정한 경로로 이동시키기

```JavaScript
<script>
...
  methods: {
    async submitForm() {
      try {
        ...
        // 특정 함수를 실행하여 페이지 이동
        this.$router.push('/main');
      } catch (error) {
        ...
  },
};
</script>
```



## 2. 컴포넌트 간 데이터 전달

1. 이벤트 - 프롭스 컴포넌트 통신 방식: 규모가 커질 수록 복잡하고 비효율적
2. 이벤트버스
3. Vuex: 가장 효율적



## 3. Vuex

### 3.1 Vuex install

```shell
npm i vuex
```



### 3.2 store 생성과 주입

```JavaScript
// src/store/index.js
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    username: '',
  },
});

```

```JavaScript
import Vue from 'vue';
import App from './App.vue';
import router from '@/routes/index';
import store from '@/store/index';

Vue.config.productionTip = false;

new Vue({
  render: h => h(App),
  router,
  // store 주입
  store,
}).$mount('#app');

```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

