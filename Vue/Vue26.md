# Vue.js - 라우터 설치 및 라우터 구현

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. vue router 설치

```shell
npm i vue-router --save
```



## 2. router 불러오기 및 적용

* 코드를 용도별로 분류하는 것이 구조파악에 좋으므로 router 전용의 디렉토리와 파일을 만들기



### src/router/index.js

```JavaScript
import Vue from 'vue';
import VueRouter from 'vue-router';
// 라우팅에 사용할 컴포넌트
import NewsView from '../views/NewsView.vue'
import AskView from '../views/AskView.vue'
import JovsView from '../views/JovsView.vue'

Vue.use(VueRouter);

// Vue Router를 관리하는 객체
export const router = new VueRouter({
  routes: [
    {
      // path: url 주소
      path: '/news',
      // component: url로 갔을 때 표시될 컴포넌트
      component: NewsView,
    },
    {
      path: '/ask',
      component: AskView,
    },
    {
      path: '/jobs',
      component: JovsView,
    },
  ]
})
```



### src/main.js

* router를 불러와서 Vue 인스턴스에 넣어주기

```JavaScript
import Vue from 'vue'
import App from './App.vue'
import { router } from './router/index.js';

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  router,
}).$mount('#app')

```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

