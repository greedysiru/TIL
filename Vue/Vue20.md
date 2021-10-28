# Vue.js - Helper

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. Helper

* Store에 있는 속성들을 더 쉽게 사용
  * state -> mapState
  * getters -> mapGetters
  * mutations -> mapMutations
  * actions -> mapActions



## 2. Helper의 사용법

*  Helper를 사용하고자 하는 vue 파일에서 아래와 같이 해당 헬퍼를 로딩

```JavaScript
// App.vue
import { mapState } from 'vuex';
import { mapGetters } from 'vuex';
import { mapMutations } from 'vuex';
import { mapActinos } from 'vuex';

export default {
  // this.num, this.countedNum으로 컴포넌트에서 접근 가능
	computed() { ...mapState(['num']), ...mapGetters(['countedNum']) },
  // 가져온 메서드 사용 가능
	methods: { ...mapMutations(['clickBtn']), ...mapActions(['asyncClickBtn']) }
}
```



# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

