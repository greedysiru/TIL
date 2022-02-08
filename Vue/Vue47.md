

# Vue.js - 컴포넌트 디자인 패턴(Slot)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. Slot

* 마크업 확장이 가능한 컴포넌트
* 부모 컴포넌트에서 마크업을 넘겨받는 컴포넌트



## 2. 사용하는 이유

* 컴포넌트를 유연하게 사용할 수 있음
  * 요구사항에 따라서 부모 컴포넌트에서 다양한 마크업을 넘길 수 있음
* 부모 컴포넌트에서 스타일링을 한 마크업을 넘길 수 있음



## 3. 예시

```Vue
// 부모 컴포넌트
<template>
	<div>
    // 자식 컴포넌트에게 '제목'이라는 문자열 넘김
    // 마크업도 가능
    <main-title>제목</title>
  </div>
</template>
...


// 자식 컴포넌트(main-title)
<template>
	<strong>
    // 부모 컴포넌트에서 '제목'이라는 문자열을 넘겨받게 됨
  	<slot>
  	</slot>
  </strong>
</template>
```

# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

