# Vue.js - Vuex 설치 및 등록, state & getters

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. Vuex 설치 및 등록

### Vuex 설치

* Vuex는 싱글 파일 컴포넌트 체계에서 NPM 방식으로 라이브러리를 설치하는 것이 좋음
* ES6와 함께 사용해야 더 많은 기능과 이점을 제공받을 수 있음

```shell
npm install vuex --save
```



### Vuex 등록

* src/store 디렉토리 생성

```javascript
import Vue from 'vue';
import Vuex from 'vuex';

// use: 플러그인 사용
// vue 사용하는 모든 영역에 특정 기능 추가
// 전역에 Vuex 사용
Vue.use(Vuex);

// export하면 다른 파일에서 접근 가능
export const store = new Vuex.Store({

});
```



* main.js에 등록

```javascript
import Vue from 'vue'
import App from './App.vue'
import {store} from './store/store';

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  // store 등록
  store,
}).$mount('#app')
```



## 2. state & getters

### Vuex 기술 요소

* state: 여러 컴포넌트에 공유되는 **data**
* getters: 연산된 state 값을 접근하는 속성 **computed**
* mutations: state 값을 변경하는 이벤트 로직, 메서드 **methods**
* actions: 비동기 로직을 선언하는 메서드 **async methods**



### state란?

* 여러 컴포넌트 간에 공유할 데이터 - 상태

```Vue
// Vue
data: {
	message: 'Hello Vue.js!'
}

// Vuex
state: {
	message: 'Hello Vue.js!'
}
```

```Vue
<!-- Vue -->
<p>
  {{ message }}
</p>

<!-- Vuex -->
<p>
  {{ this.$store.state.message }}
</p>
```



### getters란?

* state 값을 접근하는 속성이자 **computed()** 처럼 미리 연산된 값을 접근하는 속성

```Vue
// store.js
state: {
  num: 10
},
getters: {
  getNumber(state) {
    return state.num;
  },
  doubleNumber(state) {
    return state.num * 2;
  }
}
```

```Vue
<p>{{ this.$store.getters.getNumber }}</p>
<p>{{ this.$store.getters.doubleNumber }}</p>
```



# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

