# Vue.js - Vue CLI로 프로젝트 생성, ESLint

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. Vue CLI로 프로젝트 생성

```shell
vue create [프로젝트명]
```

* 프로젝트를 구성하는 패키지들의 인스톨까지 진행



### 프리셋이란?

* Vue CLI 3.x 버전 이후 부터 제공 됨
* 프로젝트를 시작하기 위한 기본적인 플러그인들의 구성



### 프로젝트 실행

```shell
npm run serve
```



## 2. ESLint

### ESLint를 사용해야 하는 이유

* 오류가 없는 코딩을 하기위한 장치
* 문장 끝 세미콜론 사용, trailing comma 등 코드 오류를 최소화하기 위해 강제

```JavaScript
// 세미콜론를 강제
// JavaScript는 기본적으로 세미콜론을 생략해도 코드를 해석할 수 있으나, 아래와 같은 경우에는 오류가 발생
if (a === 1) console.log('1이다') b() c()

// trailing comma
// 객체의 요소가 하나라도 콤마 사용을 강제
components: {
  '컴포넌트 이름': 컴포넌트 내용,
}
```



### Vue CLI 3.x에서 ESLint 설정 끄기

* **/* eslint-disable */**을 주석으로 넣으면, 해당 파일에서 ESLint는 꺼짐
* **// eslint-disable-next-line**을 주석으로 넣으면, 다음 줄을 ESLint가 검사하지 않음
* 프로젝트의 루트에 **vue.conifg.js**를 생성하여 아래를 입력

```JavaScript
// vue.config.js
module.exports = {
  lintOnSave: false,
}
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

