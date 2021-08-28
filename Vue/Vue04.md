# Vue.js - 컴포넌트 통신 방법(응용)

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 같은 컴포넌트 레벨 간의 통신 방법

* 상위 컴포넌트를 거쳐서 같은 레벨의 컴포넌트 간의 통신이 가능하다.

### 예시

```html
...
<body>
  <div id="app">
    <!-- 부모로부터 propsdata를를 받음 -->
    <app-header v-bind:propsdata="num"></app-header>
    <!-- pass이벤트 감지하여 deliverNum 메소드 호출 -->
    <app-content v-on:pass="deliverNum"></app-content>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var appHeader = {
      template: '<div>Header</div>',
      props: ['propsdata']
    }
    // pass라는 버튼을 누르면 passNum 메소드 호출
    var appContent = {
      template: '<div>Content<button v-on:click="passNum">pass</button></div>',
      methods: {
        passNum: function () {
          // pass라는 이벤트와 10을 부모로 넘김
          this.$emit('pass', 10);
        }
      }
    }
    new Vue({
      el: '#app',
      components: {
        'app-header': appHeader,
        'app-content': appContent,
      },
      data: {
        num: 0
      },
      methods: {
        deliverNum: function (value) {
          this.num = value;
        }
      }
    })
  </script>
...
```





# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

