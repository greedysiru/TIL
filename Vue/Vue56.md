

# Vue.js - 코드 스플리팅

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**

## 코드 스플리팅

* SPA 경우 모든 페이지의 정보를 첫 진입시에 받아오게 된다
  * app.js
  * 화면의 개수가 많을 때, 로딩 시간이 많이 걸리게 됨
* 코드 스플리팅을 활용하여 이동시에 필요한 페이지만 받아오도록 처리할 수 있음
  * 초기 애플리케이션 로딩이 줄어듦



### 예시

```javascript
import Vue from 'vue';
import VueRouter from 'vue-router';

// Vue.use: 플러그인을 사용
Vue.use(VueRouter);

// 인스턴스 생성 후 export
export default new VueRouter({
  // routes: 페이지의 라우팅 정보를 담는 배열
  routes: [
    {
      path: '/login',
      component: () => import('@/views/LoginPage.vue'),
    },
    {
      path: '/signup',
      component: () => import('@/views/SignupPage.vue'),
    },
  ],
});

```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)