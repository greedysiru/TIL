# Vue.js - router-view, kebab case, redirect, router-link

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. router-view

* 구성한 router를 보여줌

```Vue
<template>
  <div id="app">
    <!-- 지정한 라우트에 따라서 컴포넌트가 나타나게 됨 -->
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  methods: {
    fetchData() {
      console.log('hello');
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```



## 2. redirect

* 특정 url에서 다른 url로 이동시킴

### src/router/index.js

```JavaScript
import Vue from 'vue';
import VueRouter from 'vue-router';
import NewsView from '../views/NewsView.vue'
import AskView from '../views/AskView.vue'
import JovsView from '../views/JobsView.vue'

Vue.use(VueRouter);

// Vue Router를 관리하는 객체
export const router = new VueRouter({
  routes: [
    {
      // redirect를 설정하여 기본 페이지를 ~/news로 지정
      path: '/',
      redirect: '/news',
    },
    {
      path: '/news',
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



## 3. kebab case

* Vue에서 컴포넌트를 사용할 때는 kebab case로 사용하는 것이 권장
  * Vue 공식문서에서 Essential
  * VSC에서 자동완성 및 컴포넌트 바로가기 같은 편의 기능 사용 가능
* 파일명은 pascal case
  * Vue 공식 문서에서 Strongly Recommended

```vue
<template>
  <div id="app">
    <!-- kebab case -->
    <tool-bar></tool-bar>
    <router-view></router-view>
  </div>
</template>

<script>
// pascal case
import ToolBar from './components/ToolBar.vue';

export default {
  components: {
    // pascal case
    ToolBar,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```



## 4. router-link

* 특정 라우트로 이동시킬 a태그를 생성



### src/components/ToolBar.vue

```Vue
<template>
  <div>
    <!-- a태그로 변환되고 클래스가 부여 됨 -->
    <!-- to에 지정된 라우트로 이동 -->
    <router-link to="/news">News</router-link>
    <router-link to="/ask">Ask</router-link>
    <router-link to="/jobs">Jobs</router-link>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

