# Vue.js - 실무 환경을 위한 프로젝트 설정

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. API 설정 공통화

### axios.create

* axios의 공통 설정을 할 수 있는 api
* axios 인스턴스를 생성하여 활용할 수 있음

```JavaScript
import axios from 'axios';

// 공통 설정을 할 수 있는 api
const instance = axios.create({
  baseURL: 'http://localhost:3000',
});

```



## 2. env 파일과 설정

### 서버 엔드포인트를 환경 변수로 관리하기

* 루트에 .env 파일을 생성하여 아래처럼 입력
* VUE_APP 접두사가 붙으면 별도의 웹팩 설정 없이 접근할 수 있음
  * 원래는 webpack DefinePlugin이 필요
  * vue cli 3에서 제공하는 기능

```
VUE_APP_API_URL=http://localhost:3000/
```



### 환경 변수 가져오기

```JavaScript
import axios from 'axios';

const instance = axios.create({
  // 환경변수 접근
  baseURL: process.env.VUE_APP_API_URL,
});
...
```



## 3. Vue CLI의 env 파일 규칙

* 환경 변수를 개발용, 배포용으로 분류하여 관리
  * .env: 공통으로 사용되는 환경 변수
  * .env.development: 로컬 서버에서 사용되는 환경 변수
  * .env.production: `npm run build` 입력하였을 때 사용되는 환경 변수

# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

