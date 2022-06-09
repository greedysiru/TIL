# Vue.js - 라우터 네비게이션 가드

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 라우터 네비게이션 가드

* 특정 라우터 진입 전에 로직을 정의 가능
  * 데이터를 먼저 요청, 로딩하도록 할 수 있음
* 데이터 호출과 관련된 패턴을 구현 가능
* 특정 라우터 접근을 막을 수 있음
  * 로그인이 필요한 페이지의 접근 막기



### 글로벌 Before Guards를 위한 세팅

* 생성될 vueRouter 인스턴스를 특정 식별자에 담기

```JavaScript
import Vue from 'vue';
import VueRouter from 'vue-router';
import store from '../store';

Vue.use(VueRouter);

const router = new VueRouter({
  mode: 'history',
  routes: [
    {
      path: '/',
      redirect: '/login',
    },
    {
      path: '/login',
      component: () => import('@/views/LoginPage.vue'),
    },
    ...
  ],
});

// router를 export
export default router;
```



### 라우트 부가 정보 정의하기

* 라우트를 지정할 때, meta 프로퍼티에 특정 라우터의 부가적인 정보를 정의할 수 있음

```JavaScript
{
  path: '/main',
    component: () => import('@/views/MainPage.vue'),
      // 해당 라우터의 부가 정보
      // 해당 페이지 진입시 로그인을 체크
      meta: { auth: true },
},
```



### beforeEach 정의

* 라우트를 이동하기 전에 실행됨

```JavaScript
router.beforeEach((to, from, next) => {
  // to : 이동하려는 페이지
  // from : 출발하는 페이지
  // next : 페이지 이동하는 API
  // 이동하려는 페이지의 meta.auth가 true이면 인증 상태 검사
  // 사용자가 로그인 상태가 아닐 때 로그인 페이지로 이동
  if (to.meta.auth && !store.getters.isLogin) {
    next('/login');
    return;
  }
  next();
});
```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

