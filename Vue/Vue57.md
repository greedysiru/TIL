# Vue.js - 초기 진입 페이지 설정, Fall Back Router, History Mode

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**

## 1. 초기 진입 페이지 설정

* redirect를 설정하여, 진입되었을 때 특정 페이지로 이동

```JavaScript
import Vue from 'vue';
import VueRouter from 'vue-router';

// Vue.use: 플러그인을 사용
Vue.use(VueRouter);

// 인스턴스 생성 후 export
export default new VueRouter({
  // routes: 페이지의 라우팅 정보를 담는 배열
  routes: [
    {
      path: '/',
      // /login(로그인 페이지)로 리다이렉트
      redirect: '/login',
    },
    ...
});

```



## 2. Fall Back Router

* 없는 페이지(url) 접근 시에 라우터를 설정할 수 있음

```JavaScript
...
export default new VueRouter({
  routes: [
    ...
    {
      // * : 설정한 url을 제외한 모든 경로
      path: '*',
      component: () => import('@/views/NotFound.vue'),
    },
  ],
});

```



## 3. History Mode

* url에 '#' 제거
* '#'이 붙는 이유
  * SPA에서 URL은 클라이언트에서 관리가 되어, 서버가 URL을 없는 주소로 인식
  * 클라이언트 레벨의 라우팅 처리가 되도록 '#'가 붙게 됨



```JavaScript
...
export default new VueRouter({
  // routes: 페이지의 라우팅 정보를 담는 배열
  mode: 'history',
  routes: [
   ...
  ],
});
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

