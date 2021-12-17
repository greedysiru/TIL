# Vue.js - axios를 이용한 api 호출

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. 페이지 컴포넌트와 로직의 분리

* 페이지 역할을 하는 컴포넌트와 라우팅, fetch 로직은 분리해서 설계하는 것이 좋음
  * 컴포넌트의 레벨이 깊어지거나 설계가 바뀔 때 유연하게 대처할 수 있음



## 2. axios

### 설치

```shell
npm i axios --save
```



### axios란?

* http 통신 api를 편하게 사용할 수 있는 라이브러리
* Promise 기반으로 api 제공
  * http 메소드



## 3. axios를 이용한 api 호출

* axios는 http 메소드를 Promise 기반으로 제공
* then으로 통신 다음 처리를 콜백으로 가능
* catch로 통신 오류 다음 처리를 콜백으로 가능
* 콜백으로 화살표 함수를 쓰면, 암묵적으로 현재 Vue 인스턴스를 this로 가리킴
  * this 바인딩을 할 필요가 없음



### 예시

```Vue
...
<script>
import axios from 'axios';
export default {
  data() {
    return {
      users: []
    }
  },
  created() {
    // get에 파라미터로 url을 넘기면 해당 url로 get 메소드 실행
    axios.get('url')
      // get 메소드로 불러온 데이터를 콜백으로 처리
      // 화살표함수는 자동으로 현재 Vue 인스턴스를 바라봄
      .then((response) => {
        this.users = response.data;
        console.log(this.users);
        })
      // 에러 처리
      .catch((e) => {
        console.log(e);
      })
  }

}
</script>
...
```



### 콜백 함수에서의 Arrow Function vs. Function Declarations

* Arrow Function의 this는 언제나 상위 스코프를 가리킴
  *  Lexical this
  * 선언될 때 정적으로 결정 됨
  * 그러므로, 위 예시의 콜백 함수는 this를 바인딩 할 필요가 없었음
* Function Declarations의 this는 해당 함수가 호출될 때 동적으로 결정 됨
  * 콜백함수에서는 전역 객체 window를 가리킴
  * 위 처럼 콜백함수로 Vue 인스턴스를 가리키기 위해서는 this 바인딩을 해야 함

```Vue
...
<script>
import axios from 'axios';

export default {
  data() {
    return {
      users: []
    }
  },
  created() {
    // 함수 선언식의 콜백은 this를 바인딩 해야 함
    var vm = this;
    axios.get('url')
      .then(function (response) {
      vm.users = response.data;
    })
      // 에러 처리
      .catch((e) => {
        console.log(e);
      })
  }

}
</script>
...
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

