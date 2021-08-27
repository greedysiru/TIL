# Vue.js - 컴포넌트 통신

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. 컴포넌트 통신

* 컴포넌트를 등록했을 때, 컴포넌트 간의 관계가 생기게 된다.
  * 상위 컴포넌트 - 하위 컴포넌트
* 컴포넌트는 각각 고유한 데이터 유효 범위를 갖는다.
  * props 속성: 상위에서 하위로는 데이터를 내려줌
  * event: 하위에서 상위로는 이벤트를 올려줌



## 2. 컴포넌트 통신 규칙이 필요한 이유

* N방향 통신의 문제점
  * 특정 기능이 바뀌었을 때 그로인한 버그를 추적하기 어렵다.(MVC 패턴)
* 컴포넌트 통신 규칙
  * 데이터의 흐름을 추적할 수 있다.
  * 위에서 아래로는 props, 아래에서 위로는 event이므로



## 3. props 속성

```html
...
<body>
  <div id="app">
    // v-bind: props 속성 이름 = "상위 컴포넌트의 데이터 이름"
    <app-header v-bind:propsdata="message"></app-header>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var appHeader = {
      template: '<h1>header</h1>',
      props: ['propsdata']
    }
    new Vue({
      el: '#app',
      components: {
        'app-header': appHeader
      },
      // Root(상위 컴포넌트)에서 관리하는 data
      data: {
        message: 'hi'
      }
    })
  </script>
</body>
...
```



## 4. props 속성의 특징

* 상위 컴포넌의 data가 바뀌었을 때, props 반영되어 내려와 하위 컴포넌트가 받게 된다.
  * Reactivity
* 데이터 바인딩
  * 이중 괄호로 props를 사용할 수 있다.

```html
...
    var appHeader = {
      // 데이터 바인딩
      template: '<h1>{{ propsdata }}</h1>',
      props: ['propsdata']
    }
    new Vue({
      el: '#app',
      components: {
        'app-header': appHeader
      },
      // Root에서 관리하는 data
      data: {
        message: 'hi'
      }
    })
...
```



## 5. event emit

* **v-on**: Vue에서 제공하는 속성

```html
...
<body>
  <div id="app">
    <!-- pass라는 이벤트를 감지하여 logText 메소드 실행 -->
    <app-header v-on:pass="logText"></app-header>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var appHeader = {
      // v-on:click 클릭 이벤트
      // 하위 컴포넌트의 이벤트를 감지하여 상위 컴포넌트의 메소드를 실행
      template: '<button v-on:click="passEvent" >Click Me</button>',
      methods: {
        // 버튼이 눌렸을 때 실행되는 함수
        passEvent: function () {
          // api, pass라는 이벤트 발생
          this.$emit('pass');
        }
      }
    }
    new Vue({
      el: '#app',
      components: {
        'app-header': appHeader
      },
      methods: {
        // 메소드
        logText: function () {
          console.log('hi');
        }
      }
    });
  </script>
</body>
...
```



## 6. 뷰 인스턴스에서의 this

* 객체 안에서 다른 속성을 가져올 때 사용
* 객체 안의 this는 해당 객체를 가리킴
* 뷰 인스턴스 methods 안의 this는 해당 인스턴스 data 안을 가리킴
  * 즉 this.data안의변수명 을 입력하여 해당 값을 가져올 수 있다.

# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

