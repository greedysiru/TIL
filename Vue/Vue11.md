# Vue.js - 프로젝트 구성

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**

## 1. Vue CLI 설치

```shell
npm install -g @vue/cli
```



## 2. 프로젝트 구성

```shell
vue create [프로젝트명]
```

* 프로젝트 구성
* 여러가지 기능을 선택하여 프로젝트를 구성할 수 있음
* **npm run serve**로 프로젝트 실행



### 템플릿 적용

```shell
vue init webpack-simple vue-todo
```

* webpack-simple 템플릿이 적용된 Vue 프로젝트 생성



## 3. 컴포넌트 설계

* 페이지가 많아질 수록 컴포넌트 설계의 중요성이 높아진다.
* 컴포넌트 설계는 재사용성을 고려한다.
  * ex) 웹앱 전체 페이지에서 상단에 표시되는 헤더


# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

