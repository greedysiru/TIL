# Vue.js - Vuex(mutations, getters)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. mutations

* store의 state를 조작하는 역할

### 1.1 정의

* a태그와 같이 특정 요소를 클릭하면 지정한 경로로 이동

```JavaScript
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    username: '',
  },
  // state를 변경하는 역할
  mutations: {
    // 첫 번째 파라미터: store의 state
    // 두 번째 파라미터: commit 할때의 payload
    setUsername(state, username) {
      state.username = username;
    },
  },
});

```



### 1.2 호출

* commit으로 정의한 mutations 호출

```Vue
...
<script>
...
  methods: {
    async submitForm() {
      try {
        // 비즈니스 로직
        ...
        // mutations에 정의된 setUsername 호출
        this.$store.commit('setUsername', data.user.username);
        this.logMessage = `${data.user.username} 님 환영합니다`;
        this.$router.push('/main');
      } catch (error) {
        // 에러 핸들링할 코드
        ...
      } finally {
       ...
      }
    },
  },
};
</script>
...
```



## 2. getters

* state가 변경시 특정 상태를 계산하여 반환



### 1.1 정의

```JavaScript
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    username: '',
  },
  // state가 변경 시, 특정 상태를 계산
  getters: {
    // 첫 번째 파라미터: store의 state
    isLogin(state) {
      // getters는 기본적으로 return을 해야함
      return state.username !== '';
    },
  },
  ...
  },
});

```



### 1.2 호출

```Vue
<template>
  <header>
   ...
    <div class="navigations">
      <!-- computed에서 store의 getter를 가져와서 사용 -->
      <!-- 1. 로그인이 되었을 때 -->
      <template v-if="isUserLogin">
        <sapn class="username">{{ $store.state.username }}</sapn>
      </template>
      <!-- 2. 로그인이 안 되었을 때 -->
      <tempalte v-else>
        <router-link to="/login">로그인</router-link>
        <router-link to="/signup">회원가입</router-link>
      </tempalte>
    ...
</template>

<script>
export default {
  computed: {
    isUserLogin() {
      // 정의한 getters 가져오기
      return this.$store.getters.isLogin;
    },
  },
};
</script>
...

```







## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

