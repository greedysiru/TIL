# Vue.js - 라우터 링크 스타일링, mode history

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 라우터 링크 스타일링

### scoped

* 해당 컴포넌트에만 적용하는 스타일을 작성할 수 있음

```Vue
<template>
...
</template>

<script>
...
</script>

// 이 컴포넌트에만 적용되는 스타일
<style scoped>
  .header {
    color: white;
    background-color: #42b883;
    display: flex;
    padding: 8px;
  }
...
</style>
```



### 라우터 링크 스타일링

* 라우터 자체 내부적으로 적용되는 클래스가 있음
  * 해당 클래스에 스타일을 지정할 수 있음

```Vue
...
<style scoped>
...
  /* 라우터 자체 내부적으로 적용되는 클래스 */
  /* 활성화 된 링크 */
  .header .router-link-exact-active {
    color: #35495e;
  }
  /* 활성화가 안 된 링크 */
  .header a {
    color: white;
  }
</style>
```



## 2. mode history

* router에서 url의 해시를 제거

```JavaScript
...
Vue.use(VueRouter);

// Vue Router를 관리하는 객체
export const router = new VueRouter({
  mode: 'history',
  routes: [
    {
      path: '/',
      redirect: '/news',
    },
    ...
  ]
})
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

