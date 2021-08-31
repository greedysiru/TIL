# Vue.js - watch 속성

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. watch 속성

* data의 변화에 따라 로직을 실행



### 예시

```HTML
...
<body>
  <div id="app">
    {{ num }}
    <!-- 버튼을 누르면 addNum 메소드 호출 -->
    <button v-on:click="addNum">increase</button>
  </div>
...
  <script>
    new Vue({
      el: '#app',
      data: {
        num: 10,
      },
      // data의 변화에 따라 로직 실행
      watch: {
        // num의 변화 감지
        num: function () {
          this.logText();
        }
      },
      // data의 num에 접근하여 +1
      methods: {
        addNum: function () {
          this.num = this.num + 1;
        },
        // num이 증가할 때마다, 해당 변화를 감지하여 아래의 명령을 실행
        logText: function () {
          console.log('changed');
        }
      }
    })
  </script>
...
```



## 2. watch 속성 vs computed 속성

### watch

* 매번 실행되기 부담스러운 로직에 사용
* 데이터 요청에 적합



### computed

* 내부적으로 해당 명령을 실행
* 단순하게 값에 대한 계산을 실행
  * ex) 단순 텍스트 입력 -> 그에 대한 validation을 계산
* 대부분의 상황에서 사용 권장
  * [참고](https://vuejs.org/v2/guide/computed.html#ad)
* 캐싱



### 예시

```HTML
...
<body>
  <div id="app">
    {{ num }}
  </div>
...
  <script>
    new Vue({
      el: '#app',
      data: {
        num: 10
      },
      // num을 *2 하여 리턴
      computed: {
        doubleNum: function () {
          return this.num * 2;
        }
      },
      watch: {
        // newValue: 갱신된 값, oldValue: 이전 값
        num: function (newValue, oldValue) {
          this.fetchUserByNumber(newValue);
        }
      },
      methods: {
        fetchUserByNumber: function (num) {
          console.log(num);
          // axios.get(num);
        }
      }
    });
  </script>
</body>
...
```



## 3. computed 속성을 이용한 class 코드 작성 방법

* v-bind에 computed 속성을 넣을 수 있음
* 스크립트 단에서 클래스 반영 여부를 계산



### 예시

```HTML
...
  <style>
    .warning {
      color: red;
    }
  </style>
</head>

<body>
  <div id="app">
    <!-- 조건에 따라 class 이름을 설정 -->
    <!-- computed 속성을 클래스 바인딩에 넣을 수 있음 -->
    <p v-bind:class="errorTextColor">Hello World</p>
  </div>
...
  <script>
    new Vue({
      el: '#app',
      data: {
        isError: false,
      },
      computed: {
        // 스크립트 단에서 클래스 반영 여부를 계산
        errorTextColor: function () {
          // isError가 true이면 waring return
          return this.isError ? 'warning' : null;
        }
      }
    });
  </script>
...
```





# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

