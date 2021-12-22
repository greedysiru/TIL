# Vue.js - Vuex Actions와 Mutations

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. Actions

* Vuex에서 api 호출은 actions에서 하기
  * 비동기 호출

* Backend API를 호출하여 Mutations에 넘겨주기위한 속성
* Vuex 구조상,  actions에서 state에 바로 담을 수 없게 되어있음
* Actions는 Vue Components에서 **Dispatch라는 api로 호출 가능**



## 2. Mutations

* Vuex에서 state값을 변경하거나 입력
* Action이 일어나면 값을 전달받아 state에 변경 및 입력

![vuex](https://vuex.vuejs.org/vuex.png)



## 3. 예시

### src/store/index.js

```JavaScript
import Vue from 'vue';
import Vuex from 'vuex';
import {fetchNewsList} from '../api/index.js';

// Vuex는 플러그인 형식으로 제공
Vue.use(Vuex);

//  인스턴스
export const store = new Vuex.Store({
  state : {
    news: []
  },
  mutations: {
    // 첫번째 인자 state, 두번째 인자 action으로부터 전달받은 값
    SET_NEWS(state, news) {
      // state에 데이터 전달
      state.news = news;
    }
  },
  actions: {
    // mutation에 접근할 수 있도록 context 인자가 제공
    FETCH_NEWS(context) {
      fetchNewsList()
        .then(response => {
          // mutation에 data를 넘길 수 있음
          context.commit('SET_NEWS', response.data);
        })
        .catch(error => {
          console.log(error);
        }) 
    }
  }
})

```



### src/views/NewsView.vue

```JavaScript
<template>
  <div>
	  // store의 state에 접근
    <div v-for="item in this.$store.state.news" > {{ item.title }} </div>
  </div>
</template>

<script>


export default {
  created() {
    // action 호출
    this.$store.dispatch('FETCH_NEWS');
  }

}
</script>

<style>

</style>
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

[Vuex Docs](https://vuex.vuejs.org/#what-is-a-state-management-pattern)
