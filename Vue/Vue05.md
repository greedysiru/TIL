# Vue.js - 뷰 라우터

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. 뷰 라우터 소개와 설치

* 뷰를 이용하여 싱글 페이지 애플리케이션을 구현할 때 사용하는 라이브러리

  * 페이지 이동을 가능하게 함

* **npm install vue-router**를 입력하여 설치

  * 또는 script 태그에 패키지 소스 코드를 불러오기

  ```html
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  ```
  
  



## 2. routes 속성

* 페이지의 라우팅 정보
* 어떤 url로 이동했을 때 어떤 페이지가 뿌려질지에 대한 정보
* **배열**이며 각 요소는 페이지의 정보
  * 각 페이지의 정보는 **객체**
* 페이지 정보 객체의 key
  * path: 페이지의 url
  * component: 해당 url에서 표시될 컴포넌트

```JavaScript
...
  // 라우터 인스턴스
    var router = new VueRouter({
      // 페이지의 라우팅 정보
      routes: [
        // 페이지의 갯수만큼 객체가 필요
        {
          // 페이지의 url
          path: '/login',
          // 해당 url에서 표시될 컴포넌트
          component: LoginComponent
        },
        {
          path: '/main',
          component: MainComponent
        }
      ]
    });

    new Vue({
      el: '#app',
      // 뷰 인스턴스에 라우터 연결
      router: router

    });
...
```



## 3. router-view 태그

* url에 따라 컴포넌트를 출력할 영역
* router 패키지가 기본적으로 가진 태그
* Vue 인스턴스와 router 인스턴스를 연결해야 사용 가능

```html
...
<body>
  <div id="app">
    <router-view></router-view>
  </div>
...
```



## 4. router-link 태그

* 화면에서 링크를 제공하여 페이지 이동
* 앵커태그로 변환되어 화면에 나타남

```html
...  
	<div id="app">
    <router-link to="/login">Login</router-link>
    <router-link to="/main">Main</router-link>
    <router-view></router-view>
  </div>
...
```





# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

