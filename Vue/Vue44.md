# Vue.js - 라우터 네비게이션 가드

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 네비게이션 가드

* 라우트에서 리디렉션 또는 네비게이션을 보호하는 데에 사용
  * ex) 로그인 인증 상태가 아니면 네비게이션을 보호하고 로그인 페이지로 리다이렉팅
* 세 가지 전달 인자를 받음
  * to: 이동할 라우트 정보 객체
  * from: 출발하는 라우트 정보 객체
  * next: to 라우트로 이동시키는 **함수**



## 2. beforeEnter

* 네비게이션 가드 중 하나
* 해당 라우트에 진입하기 전의 동작을 정의할 수 있음
  * 라우트 설정 객체에 직접 정의

### 정의 방법

```JavaScript
...
Vue.use(VueRouter);

// Vue Router를 관리하는 객체
export const router = new VueRouter({
  mode: 'history',
  routes: [
    {
      // path: url 주소
      path: '/mypet',
      name: 'mypet',
      component: createListView('mypet'),
      // 3개의 인자를 받음
      beforeEnter: (to, from, next) => {
        // 해당 라우트 진입 전의 로직 또는 api 호출 등을 정의
        next();
      }
    },
...
  ]
})
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

