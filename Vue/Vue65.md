# Vue.js - 엑시오스 인터셉터

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. 엑시오스 인터셉터

* 서버로 요청 또는 서버로부터의 응답을 처리하기 전에 로직을 정의할 수 있음
* axios.interceptors.request.use
* axios.interceptors.response.use



## 2. 엑시오스 인터셉터를 활용한 HTTP Header Authorization 토큰 설정

* 엑시오스 인스턴스를 생성할 때  HTTP Header Authorization 토큰을 지정하여도, 처음 초기화 시점에서는 토큰이 없기 때문에 로그인 이후에도 토큰이 Header에 실리지 않음
* 엑시오스 인터셉터를 활용해서 Vuex에 token이 있을 때 HTTP Header Authorization 지정



### api/common/interceptors.js

* 엑시오스 인터셉터 모듈 부분을 모듈화

```JavaScript
// 스토어 가져오기
import store from '@/store/index';

export function setInterceptors(instance) {
  // 엑시오스 인터셉터
  // 넘겨받은 인스턴스에 인터셉터 정의
  // 요청 전 인터셉터
  instance.interceptors.request.use(
    function(config) {
      // store에 저장된 토큰을 요청 헤더에 싣기
      config.headers.Authorization = store.state.token;
      return config;
    },
    function(error) {
      return Promise.reject(error);
    },
  );

  // 응답 받기 전 인터셉터
  instance.interceptors.response.use(
    function(response) {
      return response;
    },
    function(error) {
      return Promise.reject(error);
    },
  );
  // 인터셉터가 정의된 인스턴스 반환
  return instance;
}

```



### api/index.js

* 모듈화된 엑시오스 인터셉터를 가져와서 헤더에 토큰이 실리도록 하기

```JavaScript
import axios from 'axios';

// 엑시오스 인터셉터 가져오기
import { setInterceptors } from './common/interceptors';

// 인스턴스를 초기화하는 함수
function createInstance() {
  // 인스턴스 생성
  const instance = axios.create({
    baseURL: process.env.VUE_APP_API_URL,
  });

  // 생성한 인스턴스를 전달하여 인터셉터가 정의된 인스턴스를 반환
  return setInterceptors(instance);
}

// 엑시오스 인터셉터를 거쳐온 엑시오스 인스턴스
const instance = createInstance();

function registerUser(userData) {
  // 매번 api가 호출될 때 마다 createInstance가 실행되어 엑시오스 인터셉터로 인해 토큰이 실리게 됨
  return instance.post('signup', userData);
}

function loginUser(userData) {
  return instance.post('login', userData);
}

export { registerUser, loginUser };

```







## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

