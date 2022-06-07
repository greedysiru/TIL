# Vue.js - 토큰

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. 토큰

* 유저가 유효한 권한을 가지고 있는지를 판별하기 위한 값
  * 401 Error: api를 요청하였을 때, 유저가 유효한 권한이 없을 경우에 발생
* 주로 로그인 이후에 서버로부터 부여받음
* JWT
  * JSON Web Token
  * JSON Object로 표현되는 토큰
  * HMAC, RSA 등의 알고리즘에의해 암호화될 수 있음 



## 2. HTTP 헤더에 토큰 값을 싣기

* axis 인스턴스를 생성할 때, HTTP Header Spec인 Authorization을 지정할 수 있음
  * token을 지정하여 API 호출 시, 권한을 인증

```JavaScript
import axios from 'axios';

const instance = axios.create({
  baseURL: process.env.VUE_APP_API_URL,
  // HTTP Header Spec
  headers: {
    // token을 실어 보냄
    // API 권한을 확인
    Authorization: 'token',
  },
});

```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

