# Vue.js - HTTP 통신 라이브러리(axios)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. axios

* Vue에서 권장하는 HTTP 통신 라이브러리
  * Promise 기반
* HTTP 통신 라이브러리들에 비해 문서화가 잘 되어 있고 API가 다양
* vue-resource
  * 예전의 공식 라이브러리
  * 샘플코드를 마주칠 수 있으니 참고



### Ajax

* Asynchronous JavaScript and XML
* 비동기적인 웹 애플리케이션 제작을 위한 웹 개발 기법
* HTML 문서에서 일부 필요한 부분만 받아올 수 있다.
  * SPA을 가능하게 하는 기술 중 하나
* jQuery.ajax()



### 오픈 소스를 사용하는 방법

* 오픈 소스 라이브러리의 깃허브를 참고하기
  * star 수 확인
  * 커밋과 contributors 확인



## 2. JavaScript의 비동기 처리 패턴

* callback
* promise
* promise + generator
* async & await



## 3. axios 실습 및 this 설명

* axios then안에서의 this는 실행컨텍스트가 달라서 Vue 객체를 가르키는 것이 아님에 주의
  * this대신 생성된 Vue 인스턴스로 접근할 것

### 예시

```JavaScript
...
  <div id="app">
    <!-- 버튼 클릭시 getData 메소드 호출 -->
    <button v-on:click="getData">get user</button>
    <div>
      {{ users }}
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: {
        users: []
      },
      methods: {
        // api 호출
        getData: function() { 
          var vm = this;
          // 유저 정보를 받아옴
          // promise
          axios.get('https://jsonplaceholder.typicode.com/users/')
            .then(function(response) {
              console.log(response.data);
            	// this로는 Vue 인스턴스가 불리지 않으므로 직접 인스턴스가 담긴 변수를 호출
              vm.users = response.data;
              // data의 user에 담기
            })
            .catch(function(error) {
              console.log(error);
            });
        }
      }
    })
  </script>
...
```



## 4. 웹 서비스에서의 클라이언트와 서버와의 HTTP 통신 구조

* 브라우저와 서버는 HTTP 통신을 주고 받는다.
  * HTTP 요청: 브라우저가 서버에게 요청하는 것
  * HTTP 응답: 서버가 브라우저에게 응답



### HTTP  통신 예시

* 브라우저가 서버에게 HTTP 요청
* 서버에서 특정 로직을 실행
* 로직에 의해 DB에서 데이터를 받아옴
* 해당 결과물을 브라우저에게 HTTP 응답

# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

