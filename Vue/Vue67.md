# Vue.js - API 모듈화, 동적 라우팅

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. API 모듈화

* 프로젝트의 규모가 커질 수록 하나의 index.js에 API를 정의하는 것은 유지 보수 측면에서 좋지 않음
* **기능 별로 모듈화를 하여 API를 정리하기**



### index.js

* 엑시오스 초기화 관련 함수들을 모으기
* 기능별로 분류된 각 모듈에서 엑시오스 인스턴스를 import하여 사용
  * ex) 회원가입 및 로그인 관련 모듈인 auth.js에서 엑시오스 인스턴스인 instance를 import하여 관련 함수들을 정의

```JavaScript
import axios from 'axios';
import { setInterceptors } from './common/interceptors';

// 엑시오스 인스턴스 초기화 함수
function createInstance() {
  return axios.create({
    baseURL: process.env.VUE_APP_API_URL,
  });
}

const instance = createInstance();

// 토큰이 필요한 경우의 API에 대한 엑시오스 인스턴스 초기화 함수
function createInstanceWithAuth(url) {
  const instance = axios.create({
    // 파라미터로 받은 url을 baseURL에 포함
    baseURL: `${process.env.VUE_APP_API_URL}${url}`,
  });
  return setInterceptors(instance);
}

// 생성된 인스턴스는 /posts를 URL에 붙이게 됨
const posts = createInstanceWithAuth('posts');

// 다른 모듈에서 엑시오스 인스턴스를 import할 수 있도록 export
export { instance, posts };
```



## 2. 동적 라우팅

* Dynamic Routing Matching
* route 인스턴스 안의 params 객체의 프로퍼티로 파라미터가 전달됨
  * 라우트 정의할 때, 콜론을 붙인 부분과 매칭되게 됨

```JavaScript
// src/routes/index.js
// 라우트 정의 파일
import Vue from 'vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);

export default new VueRouter({
  mode: 'history',
  routes: [
  ...
    {
      // 동적 라우팅
      // :id는 파라미터로 전달됨
      // 예를 들어, /post/1993 으로 이동을 하면, 해당 페이지에서 params의 id 프로퍼티에 1993이 들어오게 됨
      path: '/post/:id',
      component: () => import('@/views/PostEditPage.vue'),
    },
		...
  ],
});

```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

