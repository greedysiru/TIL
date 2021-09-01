# Vue.js - Vue CLI

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. Vue CLI

* Command Line Interface
  * 명령어를 통한 특정 액션을 수행하는 도구
* **npm install -g @vue/cli** 를 입력하여 설치
* 설치 된 내용은
  * 맥기준: **usr/local/lib/node_modules**
* Vue 애플리케이션을 만들기 위한 기본 환경 구성



### permission error

* 쓰기 권한이 없기 때문에 발생하는 에러
  * 관리자 권한이 아니어서 발생
* 명령어 앞에 **sudo**를 붙일 것



### 사용법

* 3.x대 버전 기준

```shell
// 프로젝트 생성
vue create '프로젝트 폴더 위치'

// 로컬 서버 실행
npm run serve
```



### npm run serve

* 로컬 서버를 실행
* package.json에서 scripts 속성에 정의된 명령어
  * 원래는 **vue-cli-service serve**



## 2. 프로젝트 폴더 구조

```
.
├── .gitignore
├── README.md
├── babel.config.js
├── package.json
├── node_modules
│   └── modules...
├── public
│   ├── favicon.ico
│   └── index.html
├── src
│   ├── App.vue
│   ├── assets
│   │   └── logo.png
│   ├── components
│   │   └── HelloWorld.vue
│   └── main.js
└── yarn.lock
```

### packges.json
* 라이브러리에대한 정보
* scripts 속성 안에 명령어를 정의할 수 있다.



### public/index.html
* built 파일이 자동으로 주입되는 div태그 존재
* 웹팩에 의해 src 폴더 및의 여러 파일들이 하나로 묶이거나 최소한의 파일로 묶여 주입됨



### src/main.js

```JavaScript
new Vue({
  render: h => h(App),
}).$mount('#app')
```

* Vue 인스턴스를 생성하여 import한 App 컴포넌트를 app id를 가진 element에 붙임
* render
  * Vue 내부에서 사용되는 함수
  * Template이라는 속성 정의시 내부적으로 실행되는 함수



## 3. 싱글 파일 컴포넌트

* HTML, JavaScript, CSS를 한 파일에서 관리
* .vue 확장자 사용



### 예시

```vue
<template>
  <!-- HTML -->
  <div>Header</div>
</template>

<script>
export default {
  // JavaScript - 인스턴스 옵션
  methods: {
    methods: {
      addNum: function () {
        ...
      },
    },
  },
};
</script>

<style>
/* CSS */
</style>
```



## 4. App.vue

* 싱글 파일 컴포넌트를 불러와 사용할 수 있다.

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- 불러온 컴포넌트 -->
    <!-- pascal case -->
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// 컴포넌트를 import
import HelloWorld from './components/HelloWorld.vue'

export default {
  // 인스턴스 옵션 속성 or 컴포넌트 옵션 속성
  name: 'App',
  // components에 등록
  components: {
    HelloWorld
  }
}
</script>

<style>
...
</style>

```




# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

