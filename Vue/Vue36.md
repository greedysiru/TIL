# Vue.js - 컴포넌트 공통화, 공통 컴포넌트 구현(1)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 컴포넌트 공통화

* 컴포넌트를 만들어서 컴포넌트를 반복적으로 사용하는 것이 효율적
* 설계 시, 컴포넌트 기반의 설계를 토대로 만드는 것이 좋음



## 2. 공통 컴포넌트 구현

* 라우트의 name 속성을 활용한 공통 컴포넌트 구현



### route name 속성 지정

* route에 name 속성을 지정하여 접근할 수 있음

```JavaScript
// src/routes/index.js
import Vue from 'vue';
import VueRouter from 'vue-router';
import NewsView from '../views/NewsView.vue';
import AskView from '../views/AskView.vue';
import JobsView from '../views/JobsView.vue';
...

Vue.use(VueRouter);

// Vue Router를 관리하는 객체
export const router = new VueRouter({
  mode: 'history',
  routes: [
    {
      path: '/',
      redirect: '/news',
    },
    {
      // path: url 주소
      path: '/news',
      // route 정보에 name도 들어가게 됨
      name: 'name',
      // component: url로 갔을 때 표시될 컴포넌트
      component: NewsView,
    },
    {
      path: '/ask',
      name: 'ask',
      component: AskView,
    },
    {
      path: '/jobs',
      name: 'jobs',
      component: JobsView,
    },
   ...
  ]
})
```



### 공통 컴포넌트에서의 분기 처리

```JavaScript
...
<script>
export default {
  created() {
    // action 호출
    // 이 컴포넌트가 호출된 시점에서의 라우트 정보를 가져옴, 라우트 정보의 name에 따라 분기 처리
    const name = this.$route.name;
    // name에 맞추어 적절한 action을 실행
    if (name === 'news') {
      this.$store.dispatch('FETCH_NEWS');
    } else if (name === 'ask') {
      this.$store.dispatch('FETCH_ASK');
    } else if (name === 'jobs') {
      this.$store.dispatch('FETCH_JOBS');
    } 
  },
...
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)