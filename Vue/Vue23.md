# Vue.js - 헬퍼 함수가 주는 간편함, vuex 모듈화

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. 헬퍼 함수가 주는 간편함

* store에 정의한 state, gettres, mutations, actions를 **map~ 함수**로 간편하게 가져올 수 있다.

### store.js

* src/store

```JavaScript
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

export const store = new Vuex.Store({
  state: {
    price: 100
  },
  getters: {
    originalPrice(state) {
      return state.price;
    },
    doublePrice(state): {
    	return state.price * 2;
    },
    triplePrice(state) {
      return state.price * 3;
    }
  }
});
```



### App.vue

```Vue
<template>
  <div id="root">
    <p>{{ originalPrice }}</p>
    <p>{{ doublePrice }}</p>
    <p>{{ triplePrice }}</p>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
  
export default {
  computed: {
    // spread 문법으로 store에 정의된 getters를 구조분해로 바로 가져올 수 있음
    ...mapGetters([
      'originalPrice',
      'doublePrice',
      'triplePrice'
    ]),
  }
}
</script>

<style>
</style>
```



## 2. 모듈화

### ES6의 import & Export를 이용하여 속성별로 모듈화

```JavaScript
import Vue from 'vue';
import vuex from 'vuex';
// 각 모듈별로 선언되어 있는 함수들을 가져옴
import * as getters from 'store/getters.js';
import * as mutations from 'store/mutations.js';
import * as actions from 'store/actions.js';

export const store = new Vuex.Store({
  state: {},
  getters: getters,
  mutations: mutations,
  actions: actions
})
```



### store 모듈화

* 앱이 비대해져서 1개의 store로는 관리가 힘들 때, **modules** 속성 사용
  * 동일한 성격의 데이터 속성을 기준으로 스토어 모듈화

```JavaScript
// store.js
import vue from 'vue';
import vuex from 'vuex';
import todo from 'modules/todo.js';

export const store = new Vuex.store({
  modules: {
    moduleA: todo, // 모듈 명칭 : 모듈 파일명
    todo // todo: todo
  }
})

// todo.js
const state = {};
const getters = {};
const mutations = {};
const actions = {};
```





# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

