# Vue.js - actions

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. actions란?

* 비동기 처리 로직을 선언하는 메서드
  * 비동기 로직을 담당하는 mutations
* 데이터 요청, **Promise**, ES6 async과 같은 **비동기 처리**는 모두 actions에 선언



### 예시 1

```JavaScript
// store.js
state: {
  num: 10
},
mutations: {
  doubleNumber(state) {
    state.num * 2;
  },
},
actions: {
  // context로 store의 메서드와 속성 접근
  delayDoubleNumber(context) {
    context.commit('doubleNumber');
    // 비동기 로직을 넣을 수 있음
  }
}

// App.vue
this.$store.dispatch('delayDoubleNumber');
```



### 예시 2

```JavaScript
// store.js
mutations: {
  addCounter(state) {
    state.counter++
  },
},
actions: {
  delayedAddCounter(context) {
    setTimeout(() => context.commit('addCounter'), 2000);
  }
}

// App.vue
methods: {
  incrementCounter() {
    this.$store.dispatch('delayedAddCounter');
  }
}
```



### 예시 3

```JavaScript
// store.js
mutations: {
  setData(state, fetchData) {
    state.product = fetchData;
  },
},
actions: {
  fetchProductData(context) {
    // api 호출 이후 응답을 state에 넣음
    return axios.get('https://domaion.com/products/1')
    						.then(response = context.commit('setData', response));
  }
}

// App.vue
methods: {
  incrementCounter() {
    this.$store.dispatch('fetchProductData');
  }
}
```



## 2. actions에 비동기 로직을 선언해야하는 이유

* 언제 어느 컴포넌트에서 해당 state를 호출하고, 변경했는지 규격화를 하여 확인하기 위해
  * mutations에 시간차를 두고 state를 변경하는 경우 추적하기 어려움
  * **그러므로 mutations 속성에는 동기 처리 로직만 넣어야 함**

# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

