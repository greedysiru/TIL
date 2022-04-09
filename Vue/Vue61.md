# Vue.js - validation

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. validation

* 형식 검사
* 로그인, 회원가입 기능을 구현할 때, 사용자의 입력이 유효한지 검사하는 것
  * ex) 이메일 회원 가입시 올바른 형식의 이메일을 입력했는지 확인
* 정규 표현식을 활용



## 2. E-mail Validation

### 2.1 정규 표현식으로 E-mail 유효성 검사

* 공통 모듈로 정의하여 여러 컴포넌트에 사용할 것이므로 src/utils에 파일 생성하여 validation 관련 함수 정의

```JavaScript
// src/utils/validation.js
function validateEmail(inputEmail) {
  const regex = /\S+@\S+\.\S+/;
  return regex.test(inputEmail);
}

export { validateEmail };
```



### 2.2 컴포넌트에서 유효성 검사 함수 사용하여 버튼 disabled 적용하기

* 정의한 정규 표현식을 가져와, 유효한 이메일 형식이 아니면 버튼 비활성화 처리하기

```Vue
<template>
  <div>
    <form @submit.prevent="submitForm">
      <div>
        <label for="username">id:</label>
        <input id="username" type="text" v-model="username" />
      </div>
      <div>
        <label for="password">pw:</label>
        <input id="password" type="text" v-model="password" />
      </div>
      <!-- 유효한 이메일이 아닐 때 버튼 비활성화 -->
      <button v-bind:disabled="!isUsernameValid" type="submit">
        로그인
      </button>
      <p>{{ logMessage }}</p>
    </form>
  </div>
</template>

<script>
import { loginUser } from '@/api/index';
import { validateEmail } from '@/utils/validation';

export default {
...
  // 입력받은 이메일 유효성 검사
  computed: {
    isUsernameValid() {
      return validateEmail(this.username);
    },
  },
...
```



## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

