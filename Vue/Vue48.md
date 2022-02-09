

# Vue.js - 컴포넌트 디자인 패턴(Controlled)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**





## 1. Controlled

* 결합력이 높은 컴포넌트
* 서드파티 라이브러리를 사용할 때 쉽게 컨트롤할 수 있게하는 디자인 패턴
* 원칙적으로 부모에게 넘겨받은 props는 자식 컴포넌트에서 변경 불가
  * 자식 컴포넌트에서 emit을 사용하는 이유



## 2. v-model

* Vue directive
* input event, value로 이루어짐
  * 자식 컴포넌트에서 v-model로 props를 변경 불가
* 올바른 사용법
  * 부모 컴포넌트에서 자식 컴포넌트로 v-model 사용
  * **상위에서 데이터를 관리해야 함**
    * 컴포넌트의 데이터 의존성 분리



## 3. 예시

```Vue
// 부모 컴포넌트
<template>
	<input-text v-model="text"></input-text>
</template>
<script>
	import InputText from './components/InputText.vue';
  
  export default {
    components: {
      InputText
    },
    data() {
      return {
        text: '',
      }
    }
  }
</script>
...


// 자식 컴포넌트
<template>
	<input type="text" :value="value" @input="inputText">
</template>
<script>
	export default {
    // v-model의 value
    props: ['value'],
    methods: {
      inputText(e) {
				// 컴포넌트 통신
        // v-model의 input event
        this.$emit('input', e.target.value);
      }
    }
  }
</script>
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

