# Vue.js - 싱글 파일 컴포넌트

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. 기본 형식

* .vue 확장자를 사용
* .vue 확장자 파일 생성후, vue입력하면 기본 형식이 갖춰진 코드가 입력된다.

```vue
<template>
  <!-- HTML element가 최상위에 하나만 있어야 함 -->
  <!-- data 바인딩된 str이 나옴 -->
  <div>{{ str }}</div>
</template>

<script>
export default {
  data: function () {
    // 다른 컴포넌트의 data 객체를 참조하면 안되므로 무기명 함수로 객체 return
    return {
      str: "hi",
    };
  },
};
</script>

<style>
</style>
```



## 2. 등록하기

* 일반적으로 src/componetns 경로에 싱글 파일 컴포넌트를 만든다.
* pascal case 명명법을 사용
  * 최소한 두 단어 이상으로 만들기
  * HTML 표준 태그인지 컴포넌트인지 구분하기 위해
* 가져온 컴포넌트는 kebab case를 사용

```vue
<template>
  <div>
    <app-header></app-header>
  </div>
</template>

<script>
// 싱글 파일 컴포넌트 가져오기
import AppHeader from "./components/AppHeader.vue";
export default {
  // 싱글 파일 컴포넌트 등록
  components: {
    "app-header": AppHeader,
  },
};
</script>

<style>
</style>
```



## 3. props 사용하기

* **v-bind:props 속성 이름 ="상위 컴포넌트의 데이터 이름"** 으로 프롭스 전달이 가능



## 4. event emit 구현

* v-on으로 하위 컴포넌트에서 이벤트를 감지하여 정의된 메소드를 사용 가능
  * 메소드에서 상위 컴포넌트로 이벤트를 보낼 수 있음
* v-on으로 하위 컴포넌트로부터 전달 받은 이벤트를 감지하여 정의된 메소드를 사용 가능




## 5. 예시

* 상위 컴포넌트 App.vue로부터 props를 내려받아 AppHeader.vue에서 화면 표시
* 하위 컴포넌트 AppHeader.vue에서 클릭 이벤트를 감지하여 정의된 메소드를 실행
  * 메소드는 호출 시 상위 컴포넌트로 이벤트 전달
* 상위 컴포넌트 App.vue에서 하위 컴포넌트 Appheader.vue로부터 이벤트를 감지하여 정의된 메소드를 실행
  * 메소드는 호출 시 상위 컴포넌트 data에 정의된 값을 변경
  * 변경된 값을 props로 하위 컴포넌트 AppHeader.vue로 넘기므로 화면에 변경된 문자가 반영

```vue
// App.vue
<template>
  <div>
    <!-- 하위 컴포넌트에 str을 props로 내리기 -->
    <!-- 하위 컴포넌트로부터 renew 이벤트를를 전달 받으면 renewStr 메소드 실행 -->
    <app-header 
    v-bind:propsdata="str" 
    v-on:renew="renewStr"
    ></app-header>
  </div>
</template>

<script>
// 싱글 파일 컴포넌트 가져오기
import AppHeader from "./components/AppHeader.vue";
export default {
  data: function () {
    return {
      str: "Header",
    };
  },
  // 싱글 파일 컴포넌트 등록
  components: {
    "app-header": AppHeader,
  },
  // str를 바꾸는 메소드
  methods: {
    renewStr: function () {
      this.str = "hi";
    },
  },
};
</script>

<style>
</style>
```

```vue
// AppHeader.vue
<template>
  <header>
    <!-- 전달 받은 props를 적용 -->
    <h1>{{ propsdata }}</h1>
    <!-- 버튼 클릭시 sendEvent 메소드 사용 -->
    <button v-on:click="sendEvent">send</button>
  </header>
</template>

<script>
export default {
  // 상위 컴포넌트로부터 props를 받아옴
  props: ["propsdata"],
  methods: {
    sendEvent: function () {
      // 상위 컴포넌트로 이벤트 전달
      this.$emit("renew");
    },
  },
};
</script>

<style>
</style>
```




# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

