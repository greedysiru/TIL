# Vue.js - 브라우저 저장소를 이용한 인증 값 관리

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. 브라우저 저장소

* JavaScript 레벨에서 로그인 인증값을 저장하여도, 새로고침을 했을 때 인증값이 날아가 버림
* 로그인 인증값을 브라우저 저장소에 저장
  * 새로고침을 하더라도 브라우저 저장소에 저장된 로그인 인증값에 접근 가능
  * 로그인 인증값과 같은 경우, 브라우저의 쿠키 저장소를 사용
* 브라우저 저장소는 아래와 같은 것들이 있음
  * 로컬스토리지
  * 세션
  * 쿠키
  * 상황에 맞게 필요한 브라우저 저장소를 사용



## 2. 인증값 보존

* 쿠키 저장소를 활용하여, 로그인 인증값을 보존



### 2.1 Cookie 관련 모듈 정의

* 쿠키 저장소에 관련된 모듈을 한 파일에 정의

```JavaScript
function saveAuthToCookie(value) {
 ...
}

function saveUserToCookie(value) {
 ...
}
...
export {
  saveAuthToCookie,
  saveUserToCookie,
 ...
};

```



### 2.2 로그인 로직 Vuex Action 정의

* 컴포넌트 단에서 비지니스 로직 노출을 줄이기
* 컴포넌트 단에서의 코드를 최대한 정리하여 UI에 관련된 로직만 처리하도록 하기

```JavaScript
...
// 쿠키 모듈 import
import {
  getAuthFromCookie,
  getUserFromCookie,
  saveAuthToCookie,
  saveUserToCookie,
} from '@/utils/cookies';
import { loginUser } from '@/api/index';

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    // 쿠키 저장소에 접근하여 username과 token이 있으면, 해당 값으로 초기화
    username: getUserFromCookie() || '',
    token: getAuthFromCookie() || '',
  },
  getters: {
    ...
  },
  mutations: {
    ...
  },
  actions: {
    // 로그인을 했을 때 발생하는 액션 정의
    // 컴포넌트 내에서 많은 로직을 action에 정리
    async LOGIN({ commit }, userData) {
      // api 호출
      const { data } = await loginUser(userData);
      saveAuthToCookie(data.token);
      saveUserToCookie(data.user.username);
    },
  },
});

```

```vue
<template>
  ...
</template>

<script>
...
export default {
  ...
  methods: {
    async submitForm() {
      try {
        // 비즈니스 로직
        const userData = {
          username: this.username,
          password: this.password,
        };
        // 비동기 처리
        // 로그인 액션 호출 후 다음 라인을 실행하도록 하기 위해 await
        await this.$store.dispatch('LOGIN', userData);
        this.$router.push('/main');
      } catch (error) {
        // 에러 핸들링할 코드
        console.log(error.response.data);
        this.logMessage = error.response.data;
      } finally {
        this.initForm();
      }
    },
    initForm() {
      this.username = '';
      this.password = '';
    },
  },
};
</script>

<style>
...
</style>

```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

