# Vue.js - 동적 라우트 매칭 원리 및 적용

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 동적 라우트 매칭이란?

* 특정 라우트로 이동할 때 특정 파라미터를 넘길 수 있음
* 파라미터에 따른 페이지를 구현할 수 있음
  * ex) 문서 번호를 파라미터로 넘겨서 문서 번호에 따른 페이지 구현
* 페이지에서의 특정 정보를 가지고 다음 페이지로 이동



## 2. 동적 라우트 매칭 적용

### 라우트 정의

* 이동시킬 경로와 컴포넌트를 정의
  * url 뒤에 **:파라미터명**을 붙여서 페이지 이동시에 매칭시킬 파라미터를 정의
  * 특정 페이지에서 해당 경로로 이동시킬 때 뒤에 파라미터를 전달 시킬 수 있게 됨

```JavaScript
// src/routes/index.js
import Vue from 'vue';
import VueRouter from 'vue-router';
...
import UserView from '../views/UserView.vue';


Vue.use(VueRouter);

// Vue Router를 관리하는 객체
export const router = new VueRouter({
  mode: 'history',
  routes: [
   ...
    {
      // :id는 라우트 매칭을 할 파라미터
      path: '/user/:id',
      component: UserView,
    }
  ]
})
```



### 파라미터 넘기기

* 페이지에서 정의한 라우트로 이동시킬 때 파라미터를 넘길 수 있음
* 넘겨 받은 파라미터를 라우트에 해당하는 컴포넌트에서 접근 가능
  * 파라미터에 따라서 컴포넌트의 화면을 구현할 수 있음
  * ex) 파라미터를 전달받아 그에 따른 api 호출 -> UI 구현

```JavaScript
// src/views/NewsView.vue
<template>
  <div>
    <p v-for="item in this.$store.state.news" >
       <a v-bind:href="item.url">
         {{ item.title }}
       </a>
       <small>
          {{ item.time_ago }} by
          <!-- user 이동할 때 item.user에 대한 정보도 넘김 -->
          <router-link v-bind:to="`/user/${item.user}`">
            {{ item.user }}
          </router-link>
        </small>
    </p>
  </div>
</template>
...
```



## 3. 라우터 Params 접근

* route에 담긴 파라미터를 접근할 수 있음
* **vueComponent** 객체의 **$route.params**에 파라미터들이 담기게 됨

```JavaScript
...
<script>

export default {
...
  created() {
    const {userName} = this.$route.params;
  },
}
...
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)