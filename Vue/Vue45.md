# Vue.js - 외부 라이브러리 모듈화, ref, 플러그인화

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 외부 라이브러리 모듈화

* 라이브러리가 공식적으로  Vue.js를 지원하지 않더라도 모듈화, 플러그인화여 사용에 용이하게 하기
* 컴포넌트 통신을 활용해서 컴포넌트 모듈을 제작
  * 부모 컴포넌트에서 비지니스 로직을 돌리고 자식 컴포넌트는 최대한 로직을 빼서 만들기
* 라이브러리의 사용법을 보며 Vue.js에 맞게 적용



## 2. ref

* Reference
* Vue.js에서 DOM을 가져오는 방법
* 각각의 뷰 컴포넌트에서만 접근 가능한 접근자
  * 다른 컴포넌트의 DOM 요소와 겹치지 않음



### 예시

```Vue
<template>
    <canvas ref="chart"></canvas>
</template>

<script>
	mouted() {
    const chart = this.$refs.chart;
  }
</script>
<style>

</style>
```



## 3. 플러그인화

* 라이브러리를 사용하는 컴포넌트가 많아질 수록 불필요한 로직과 코드가 생기게 됨
* 플러그인으로 모듈화하여 정리
* **인스턴스가 생성되었을 때, 모든 컴포넌트에서 사용할 기능을 정의하는 것**
  * Vue.use : 플러그인 초기 설치
  * prototype을 사용해, Vue 객체 속성을 확장



### 예시 및 설명

```JavaScript
// src/plugins/ExamplePlugin.js
// 불러올 공통 라이브러리
import Example from 'example.js';

export default {
  install(Vue) {
    // $_: Vue.js 스타일 가이드에서 제안한 플러그인, 함수의 prefix
    // 사용할 컴포넌트에서 this.$_Example로 접근 가능해짐
    Vue.prototype.$_Example = Exmaple;
  }
}
```



```javascript
// src/main.js
import Vue from 'vue'
import App from './App.vue'
import ChartPlugin from './plugins/ExamplePlugin.js';

Vue.config.productionTip = false

// install();
Vue.use(ExamplePlugin);

new Vue({
  render: h => h(App),
}).$mount('#app')
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

