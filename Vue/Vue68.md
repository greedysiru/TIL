# Vue.js - 뷰 필터

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 뷰 필터

* 애플리케이션의 데이터 형식을 일관성있게 적용할 때 유용
  * 데이터 포매팅은 한 컴포넌트보다 여러 컴포넌트에서 사용하기 때문에, 필터를 전역으로 등록
* filters에 등록하여 사용 가능



### 컴포넌트 필터

```vue
// 컴포넌트
<template>
  <li>
    ...
    <div class="post-time">
      <!-- API를 호출하여 받은 컨텐츠의 작성일을 등록한 로컬 필터 formatData를 통해 포매팅 -->
      {{ postItem.createdAt | formatDate }}
    </div>
		...
</template>

<script>
export default {
  ...
  // 컴포넌트(로컬) 필터 등록
  filters: {
    formatDate(value) {
      return new Date(value);
    },
  },
 ...
};
</script>
...
```



### 전역 필터

#### src/utils/filters.js

* 전역에서 필터를 사용하기 위해 별도의 파일로 모듈화

```JavaScript
export function formatDate(value) {
  return new Date(value);
}
```



#### src/main.js

* 아래와 같이 Vue 인스턴스 생성 시에 필터를 가져오면, 각 컴포넌트에서 필터 사용 가능

```JavaScript
...
import { formatDate } from '@/utils/filters';

// 필터 전역 설정
Vue.filter('formatDate', formatDate);

new Vue({
  render: h => h(App),
  router,
  store,
}).$mount('#app');

```







## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

