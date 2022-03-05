

# Vue.js - Vue Router

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**

## 1. Vue Router 설치 및 연결

### 1.1 패키지 설치

```shell
npm i vue-router
```



### 1.2 Vue Router 인스턴스 생성

* Vue Router를 플러그인 등록하고 인스턴스를 생성하여 export

```JavaScript
// src/routes/index.js
import Vue from 'vue';
import VueRouter from 'vue-router';

// Vue.use: 플러그인을 사용
Vue.use(VueRouter);

// 인스턴스 생성 후 export
export default new VueRouter();
```



### 1.3 Vue Router 연결

* 생성된 Vue Router 인스턴스를 Vue에 여녈

```JavaScript
// src/main.js
import Vue from 'vue';
import App from './App.vue';
// router 인스턴스 불러오기
import router from '@/routes/index';

Vue.config.productionTip = false;

new Vue({
  render: h => h(App),
  router,
}).$mount('#app');

```



## 2. 페이지 라우트 등록 및 연결

### 2.1 라우트 정의

* Vue Router 인스턴스에서 페이지들의 라우트 정보를 정의
  * routes라는 배열안에 객체 단위로 정의
  * 객체는 path, component라는 프로퍼티를 가짐

```JavaScript
// src/routes/index.js
...
export default new VueRouter({
  // routes: 페이지의 라우팅 정보를 담는 배열
  routes: [
    {
      path: '/login',
      component: LoginPage,
    },
    {
      path: '/signup',
      component: SignupPage,
    },
  ],
});
...
```



### 2.2 라우트 연결

```Vue
<template>
  <div id="app">
    <header>
      <!-- 라우트 연결 -->
      <router-link to="/login">로그인</router-link>
      <router-link to="/signup">회원가입</router-link>
    </header>
    <!-- 라우트의 view가 뜨는 부분 -->
    <router-view></router-view>
  </div>
</template>
...
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)