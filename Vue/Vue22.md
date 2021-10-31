# Vue.js - mapMutations, mapActions, 헬퍼의 유연한 문법

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1.Vue에서 권고하는 방식

* template 안에서는 가급적 JavaScript 연산을 줄이기
* template를 깔끔하게 표현



## 2. mapMutations

* Vuex에 선언한 mutations 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼

```JavaScript
// App.vue
import { mapMutations } from 'vuex';

methods: {
  ...mapMutations(['clickBtn']),
  atuhLogin() {},
    displayTable() {}
}

// store.js
mutations: {
  clickBtn(state) {
    alert(state.msg);
  }
}
```

```HTML
<button @click="clickBtn">popup message</button>
```



## 3. mapActions

* Vuex에 선언한 actions 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼

```JavaScript
// App.vue
import { mapActions } from 'vuex';

methods: {
  ...mapActions(['delayClickbtn']),
}
  
// store.js
actions: {
  delayClickBtn(context) {
    setTimeout(() => context.commit('clickBtn'), 2000);
  }
}
```

```HTML
<button @click="delayClickBtn">delay popup message</button>
```



## 4. 헬퍼의 유연한 문법

### Vuex에 선언한 속성을 그대로 컴포넌트에 연결하는 문법

```JavaScript
// 배열 리터럴
...mapMutations([
  'clickBtn', // 'clickBtn': clickBtn
  'addNumber' // addNumber(인자)
])
```



### Vuex에 선언한 속성을 컴포넌트의 특정 메서드에다가 연결하는 문법

```JavaScript
// 객체 리터럴
...mapMutations({
  popupMsg: 'clickBtn' // 컴포넌트 메서드 명 : store의 뮤테이션 명
})
```





# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

