# Vue.js - 이벤트 버블링, api 호출과 비동기 처리

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**

## 1. 이벤트 버블링

* 자식 요소에서 이벤트가 일어났을 때 상위 요소로 이벤트가 전달되는 것
  * @submit: submit 이벤트를 감지하여 메서드 실행
  * prevent: 이벤트 실행 후 폼의 기본적인 동작을 막음


```vue
<template>
  <!-- 이벤트 버블링에 의해 button의 submit 이벤트 감지하여 메소드 실행 -->
  <!-- prevent: submit 이벤트 실행 후 폼의 기본적인 동작(새로고침)을 막음 -->
  <form @submit.prevent="submitForm">
    <div>
      <label for="username">id: </label>
      <input id="username" type="text" v-model="username" />
    </div>
    <div>
      <label for="password">pw: </label>
      <input id="password" type="text" v-model="password" />
    </div>
    <div>
      <label for="nickname">nickname: </label>
      <input id="nickname" type="text" v-model="nickname" />
    </div>
    <button type="submit">회원 가입</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      nickname: '',
      // log
      logMessage: '',
    };
  },
  methods: {
    submitForm() {
      console.log('폼 제출');
    },
  },
};
</script>

```



## 2. api 호출과 비동기 처리

### 2.1 api 폴더 생성

* api를 호출하기 위해서 각 컴포넌트에서 aixos를 매번 import하는 것보다 한 곳에 정리하는 것이 좋음
* index.js와 같은 한 파일에 api 함수들을 정의하여 export
* api 함수는 axios(promise)를 return

```JavaScript
// src/api/index.js
import axios from 'axios';

function registerUser(userData) {
  // api endpoint
  const url = 'http://localhost:3000/signup';
  // promise return
  return axios.post(url, userData);
}

export { registerUser };

```



### 2.2 비동기 처리

* api를 호출하는 컴포넌트의 메서드에서 비동기 처리를해야 정상적으로 api 응답에 접근할 수 있음
* 메서드에 async를 정의
* await는 Promise가 reject 또는 fulfill될때까지 async 함수의 실행을 일시 정지 함

```vue
<template>
...
</template>

<script>
// api 함수 import
import { registerUser } from '@/api/index';
export default {
  data() {
    return {
      username: '',
      password: '',
      nickname: '',
      // log
      logMessage: '',
    };
  },
  methods: {
    // 비동기 처리
    async submitForm() {
      console.log('폼 제출');
      const userData = {
        username: this.username,
        password: this.password,
        nickname: this.nickname,
      };
      // promise 처리가 끝날 때까지 기다리고 응답을 받아옴
      const { data } = await registerUser(userData);
      console.log(data.username);
      this.logMessage = `${data.username}님이 가입되었습니다.`;
      // 가입 완료 후 초기화
      this.initForm();
    },
    initForm() {
      // 초기화
      this.username = '';
      this.password = '';
      this.nickname = '';
    },
  },
};
</script>
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

