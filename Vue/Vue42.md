# Vue.js -  Mixin

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. Mixin

* 공통 사용 로직, 기능들을  재사용하는 방법
* 컴포넌트 코드를 깔끔하게 정리할 수 있음
* 컴포넌트들에서 공통적으로 사용되는 로직을 정리할 수 있음
  * 비즈니스 로직만 각 컴포넌트에 남길 수 있음



## 2.  vs. HOC

* HOC의 단점
  * 컴포넌트의 레벨이 깊어짐
  * 컴포넌트 통신이 불편해질 수 있음



## 3. Mixin 형식

* Mixin을 주입할 컴포넌트의 mixins 속성을 선언 후, 배열 안에 넣기
  * 혹은 인스턴스



### 예시

```vue
const myPetMixin = {
  data() {
    return {
      petName: 'siru',
      isCat: true
    }
  },
  methods: {
    showPetName() {
      console.log(this.petName);
    }
  }
}

// component.vue
...
<script>
  import {myPetMixin} from './mixins.js';
  
  export default {
    mixins: [myPetMixin],
    ...
  }
</script>
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

