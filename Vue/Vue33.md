# Vue.js - Vuex Helper, 스토어 속성 모듈화

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. Vuex Helper

* Vuex의 속성이나 메서드를 쉽게 사용할 수 있도록 도와주는 함수들



### mapState

* 컴포넌트에서 state에 좀더 쉽게 접근할 수 있게하는 Helper

```Vue
<template>
  <div>
    <div v-for="item in ask"> {{ item.title }} </div>
  </div>
</template>

<script>
import {mapState} from 'vuex';
export default {
  computed: {
    // store의 state에 접근하여 ask를 가져옴
    // spread 연산자로 computed에 ask를 뿌림
    ...mapState({
      ask: state => state.ask,
    }),
  },
  created() {
    this.$store.dispatch('FETCH_ASK');
  },
}
</script>

<style>

</style>
```



### mapGetters

* store의 getters를 쉽게 사용할 수 있게하는 Helper
  * getters: store에서의 computed

```JavaScript
// src/store/index.js
...
export const store = new Vuex.Store({
  state : {
    news: [],
    jobs: [],
    ask: [],
  },
  // computed와 동일한 속성
  getters: {
    fetchedAsk(state) {
      return state.ask;
    }
  },
  mutations: {
    ...
  },
  actions: {
  ...
    }
  },
})

// src/views/AskView.vue
...
<script>
import {mapGetters} from 'vuex';
export default {
  computed: {
    // store에 정의된 getters에 접근(문자열로 지정)
    ...mapGetters({
      'fetchedAsk'
    })
  },
...
```



## 2. 스토어 속성 모듈화

* state, getters, mutations, actions가 많아질 수록 코드의 가독성은 떨어지고 유지보수는 힘들어짐
  * 별도의 파일로 모듈화 하는 것이 편함
  * actions.js, mutations.js 파일에 각 코드를 옮기기

# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

