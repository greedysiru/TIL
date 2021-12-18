# Vue.js - axios의 api 함수 구조화 방법, created & beforeMount

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. api 함수 구조화

* api를 사용하여 데이터를 가져와야할 때, 컴포넌트에서 매번 axios를 불러오고 api를 호출하는 것은 비효율적
* 별도의 폴더를 만들어 모듈화를 하면 효율적으로 사용할 수 있음
* HTTP Request & Response와 관련된 설정을 할 수 있음
* 사용할 api가 많아질 수록 모듈화를 하면 유용
* 여러 컴포넌트에서 쉽게 api 호출 함수를 불러올 수 있음



### 예시(src/api/index.js)

```JavaScript
// package.json에 등록된 모듈을 가져옴 (node_modules 디렉토리의 모듈)
import axios from 'axios';

// config
// 1. HTTP Request & Response와 관련된 기본 설정
const config = {
  baseUrl: 'https://api.hnpwa.com/v0/'
}

// 2. api 함수들을 정리
function fetchNewsList() {
  return axios.get(`${config.baseUrl}news/1.json`);
}

function fetchJobsView() {
  return axios.get(`${config.baseUrl}jobs/1.json`);
}

function fetchAskView() {
  return axios.get(`${config.baseUrl}ask/1.json`);
}

// 3. 내보내기
export {
  fetchNewsList,
  fetchJobsView,
  fetchAskView,
}
```



## 2. created & beforeMount

* Vue의 Life cylce hook
* api를 통해 데이터를 요청할 때는 created 또는 beforeMount에서 실행
* created: 컴포넌트가 생성되지마자 실행
* berforeMount: 컴포넌트가 생성되기 전에 실행
* 컴포넌트가 만들어지고 난 후 데이터 요청을 하면, Vue의 Reactivity로 인해 화면이 다시 그려짐



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

