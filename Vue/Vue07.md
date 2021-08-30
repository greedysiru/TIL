# Vue.js - 템플릿 문법

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. 템플릿 문법

* Vue로 화면을 조작하는 방법
* 데이터 바인딩
* 디렉티브



### 데이터 바인딩

* Vue 인스턴스에서 정의한 속성들을 화면에 표시

```JavaScript
<div> {{ message }} </div>
...
new Vue({
  data: {
    message: 'Hello Vue.js'
  }
})
...
```



### 디렉티브

* Vue에서의 HTML태그의 v-로 시작하는 속성
  * v-if



## 2. computed 속성

* 계산된 속성
* 바뀌는 값을 정의할 때 사용

```HTML
...
  <div id="app">
    <p>{{ num }}</p>
    <p> {{ doubleNum }} </p>
  </div>
...
  <script>
    new Vue({
      el: '#app',
      data: {
        num: 10,
      },
      // 바뀌는 값을 정의할 때  사용
      // 계산된 속성
      computed: {
        doubleNum: function () {
          return this.num * 2;
        }
      }
    })
  </script>
...
```



## 3. 뷰 디렉티브

### v-bind

* 화면에 표시되는 텍스트뿐만 아니라 전체적인 DOM의 정보들을 reactive하게 바꿀 수 있다.

```HTML
...
  <div id="app">
    <!-- data의 uuid를 아래 태그에 바인딩 -->
    <!-- 아래의 태그는 abc를 id로, text-blue를 class로 가지게 된다. -->
    <p v-bind:id="uuid" v-bind:class="name">{{ num }}</p>
  </div>
...
  <script>
    new Vue({
      el: '#app',
      data: {
        uuid: 'abc',
        name: 'text-blue'
      },
    })
  </script>
...
```



### v-if, v-else

* 조건부로 태그를 보여줄 지, 안 보여줄지를 분기할 수 있다.

```HTML
...
    <!-- loading이 true이면 표시 -->
    <div v-if="loading">
      Loading...
    </div>
    <!-- loading이 false이면 표시 -->
    <div v-else>
      test user has been logged in
    </div>
  </div>
...
<script>
    new Vue({
      el: '#app',
      data: {
        loading: true,
      },
    })
</script>
...
```



### v-show

* v-if와 유사하나 dom의 정보를 유지
  * v-if는 출력하지 않을 때 dom의 정보를 없앰



### v-model

* 입력을 받는  ui요소와 Vue data 속성을 연결
* v-bind, v-on 기능의 조합으로 동작

```HTML
...
    <input type="text" v-model="message">
    <p>Message is: {{ message }}</p>
...
  <script>
    new Vue({
      el: '#app',
      data: {
        message: '',
      },
    })
  </script>
...
```



## 4. methods 속성

### v-on

* 이벤트를 감지하여 메소드를 실행
* event modifier를 지정할 수 있다.

```HTML
...
<body>
  <div id="app">
    <!-- 클릭시 메소드를 실행 -->
    <button v-on:click="logText">click me</button>
    <!-- 키입력시 메소드를 실행 -->
    <input type="text" v-on:keyup="logText">
    <!-- event modifier -->
    <!-- 엔터를 눌렀을 때만 메소드 실행 -->
    <input type="text" v-on:keyup.enter="logText">
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      // 이벤트를 다루는 메소드
      methods: {
        logText: function () {
          console.log('clicked');
        }
      }
    })
  </script>
...
```

# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

