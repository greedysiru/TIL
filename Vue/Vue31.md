# Vue.js - Vuex, Vuex 모듈화 및 state 적용

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1.  Vuex

* Vue의 상태(State)관리 도구
  * 상태: 여러 컴포넌트 간에 공유되는 데이터 속성
* 서비스가 복잡해 졌을 때, 데이터를 다른 컴포넌트에 공유해야할 수도 있음
  * 컴포넌트 레벨이 깊어지거나 관계가 복잡했을 때 상태관리 도구는 유용하게 사용
* 컴포넌트에서 API를 불러와 화면을 그리는 것이 아닌, Vuex에서 API를 불러옴
  * Vuex의 State에 API로 부터 받아온 데이터를 담음
  * State를 컴포넌에 전달하여 화면을 그림



### Vuex 설치

```shell
npm i vuex
```



## 2. Vuex 모듈화 및 state 적용

### Vuex 모듈화

* Vuex와 관련된 코드를 별도의 폴더에 정리하여 모듈화

```JavaScript
// src/store/index.js
import Vue from 'vue';
import Vuex from 'vuex';

// Vuex는 플러그인 형식으로 제공
Vue.use(Vuex);

// Vuex 인스턴스
export const store = new Vuex.Store({
  state : {
    news: []
  }
})

```



### Vuex 모듈 Vue에 적용하기

```JavaScript
// src/main.js
import Vue from 'vue'
import App from './App.vue'
import { router } from './routes/index.js';
import { store } from './store/index.js';

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  router,
  store,
}).$mount('#app')
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

