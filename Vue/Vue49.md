

# Vue.js - 컴포넌트 디자인 패턴(Renderless)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. Renderless

* 데이터 처리 컴포넌트
* 템플릿이 없고 스크립트에서 비즈니스 로직만 있는 컴포넌트
  * 데이터 제공만을 하는 컴포넌트



## 2. Render Function

### template 속성

* Vue 인스턴스의 속성
* Vue 인스턴스의 마크업을 Render

```JavaScript
new Vue({
	el: '#app',
	data: {
		message: 'Hello World',
	}
	template: '<div>{{ message }}</div>'
})
```



### render

* template를 내부적으로 구현하는 함수
* createElement를 기본 인자로 받음(콜백)
  * 태그 명, 태그 속성, 하위 태그를 인자로 받는 함수

```JavaScript
new Vue({
	el: '#app',
	render: function(createElement) {
  	return createElement('div', 'Hello World');
	}
})
```



### render function의 ES6 표현

* 화살표 함수와 return 생략을 활용하여 아래처럼 간단히 표현할 수 있음

```JavaScript
new Vue({
	el: '#app',
	render: h => h(App),
})
```



## 3. Renderless Component - 구현 방법과 활용처

### 구현 방법

* 데이터를 불러오는 로직을 컴포넌트로 분리
  * 이 컴포넌트는 template도 없이 오로지 데이터만 불러옴
* 자식 컴포넌트에서 상위 컴포넌트로 불러온 데이터를 전달
  * $scopedSlots로 전달
* 상위 컴포넌트에서 하위컴포넌트로부터 받아온 데이터를 다룰 수 있음
  * v-slot directive로 접근

### 

### 예시

```vue
// 부모 컴포넌트
<template>
  <div>
    // renderless 컴포넌트
    <fetch-data>
      <!-- fetch-data 컴포넌트에서 불러온 데이터에 접근할 수 있음 -->
      <div v-slot="{response, loading}">
        <div v-if="!loading">
          {{ response }}
        </div>
        <div v-if="loading">
          loading...
        </div>
      </div>
    </fetch-data>
  </div>
</template>
...

// 자식 컴포넌트
<script>
export default {
...
  created() {
    axios.get(url)
     ...
  },
  render() {
    // 상위 컴포넌트로 데이터 전달
    return this.$scopedSlots.default({
      response: this.response,
      loading: this.loading,
    });
  },
}
</script>
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

