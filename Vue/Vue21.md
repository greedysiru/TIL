# Vue.js - mapState, mapGetters

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. mapState

* Vuex에 선언한 state 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼

```JavaScript
// App.vue
import { mapState } from 'vuex';

computed() {
  ...mapState(['num'])
  // num() { return this.$store.state.num; }
}

// store.js
state: {
  num: 10
}
```

```HTML
<!-- <p>{{ this.$store.state.num }}</p> -->
<p>{{ this.num }}</p>
```



## 2. mapGetters

* Vuex에 선언한 getters 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼

```JavaScript
// App.vue
import { mapGetters } from 'vuex';

computed() { ...mapGetters(['reverseMessage']) }

// store.js
getters: {
  reverseMessage(state) {
    return state.msg.split('').reverse().join('');
  }
}
```

```HTML
<!-- <p>{{ this.$store.getters.reverseMessage }}</p> -->
<p>{{ this.reverseMessage }}</p>
```



# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

