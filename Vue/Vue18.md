# Vue.js - mutations & commit

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. mutations이란?

* state의 값을 변경할 수 있는 **유일한 방법**이자 메서드
* mutations은 **commit()**으로 동작

```Vue
// store.js
state: { num: 10 },
mutations: {
  printNumbers(state) {
    return state.num
  },
  sumNumbers(state, anotherNum) {
    return state.num + anotherNum;
  }
}

// App.vue
this.$store.commit('printNumbers');
this.$store.commit('sumNumbers', 20);
```



## 2. mutations의 commit() 형식

* state를 변경하기 위해 mutations를 동작시킬 때 인자(payload)를 전달할 수 있음

```Vue
// store.js
state: { storeNum: 10 },
mutations: {
  modifyState(state, payload) {
    console.log(payload.str);
    return state.storeNum += payload.num;
  }
}

// App.vue
this.$store.commit('modifyState', {
  str: 'passed from payload',
  num: 20
})
```



## 3. mutations로 상태를 변경해야 하는 이유

* 특정 시점에 어떤 컴포넌트가 state를 접근하여 변경한 건지 확인하기 어렵기 때문
* 따라서, 뷰의 반응성을 거스르지 않게 명시적으로 상태 변화를 수행
  * 반응성, 디버깅, 테스팅 혜택

# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

