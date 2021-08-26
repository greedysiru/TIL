# Vue.js - 뷰 인스턴스, 컴포넌트

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 시작하기 - Age of Vue.js 강의를 토대로 작성하였습니다.**



## 1. 뷰 인스턴스

* 뷰로 개발할 때 필수로 생성해야 하는 코드이자 단위



### 인스턴스 생성

```html
...
<body>
  <div id="app">
    <!-- 뷰의 기능과 속성이 유효해진다. -->
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var vm = new Vue({
      // body태그 안에서 app이라는 아이디를 가진 태그를 찾아 인스턴스를 붙임
      el: '#app',
      data: {
        message: 'hi',
      }
    });
  </script>
</body>
...
```

* 인스턴스를 생성하고 나면 변수 안에 인스턴스의 내용을 담을 수 있다.
  * Vue가 제공하는 API와 속성이 담기게 된다.
* 인스턴스 생성 시, el에 특정 태그를 지정해야 Vue를 사용할 수 있게 된다.
  * 기본적으로 Root 컴포넌트가 된다.



### 인스턴스와 생성자 함수

```html
function Person(name, job) {
  this.name = name;
  this.job = job;
}

var p = new Person('josh', 'developer');
```

* 생성자 함수의 작명법은 Pascal Case
* 함수를 이용해서 어떤 정보를 담은 객체를 생성
* 생성자 함수를 사용함으로써, 미리 정의해놓은 기능과 속성을 사용할 수 있다.
* 인스턴스: 생성자 함수로 생성된 컴퓨터 저장공간에 할당된 실체



### 인스턴스 옵션 속성

```html
new Vue({
  el: ,
  template: ,
	data: ,
  mehtods: ,
  created: ,
  watch: ,
});
```

* el: 인스턴스가 그려지는 화면의 시작점(HTML 태그)
* template: 화면에 표시할 요소 (HTML, CSS 등)
* data: 뷰의 반응성 (Reactivity)가 반영된 데이터 속성
* methods: 화면의 동작과 이벤트 로직을 제어하는 메서드
* created: 뷰의 라이프 사이클과 관련된 속성
* watch: data에서 정의한 속성이 변화했을 때 추가 동작을 수행하 수 있게 정의하는 메서드



## 2. 컴포넌트

### 컴포넌트란

* 화면의 영역을 구성하는 단위
  * 화면의 영역을 구분하여 개발
* 코드의 재사용성이 올라가고 빠르게 화면을 제작 가능
* 영역을 구분했을 때 컴포넌트 간의 관계가 생긴다.



### 전역 컴포넌트 등록

* Vue 인스턴스를 생성하고 el에 특정 태그를 지정하면, 기본적으로 Root 컴포넌트가 된다.
* **Vue.component** 로 전역 컴포넌트를 등록할 수 있다.

```html
...
<body>
  <div id="app">
    <app-header></app-header>
    <app-content></app-content>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    // Vue.component('컴포넌트 이름', 컴포넌트 내용);
    // 컴포넌트 등록
    Vue.component('app-header', {
      template: '<h1>Header</h1>'
    });

    Vue.component('app-content', {
      template: '<div>content</div>'
    })
    new Vue({
      el: '#app',
    });
  </script>
...
```



### 지역 컴포넌트 등록

```html
...
    new Vue({
      el: '#app',
      components: {
        'app-footer': {
          template: '<footer>footer</footer>'
        }
      }
    });
...
```



### 전역 컴포넌트와 지역 컴포넌트의 차이점

* 지역 컴포넌트: 서비스 구현시 지역 컴포넌트를 주로 사용(일반적으로)
* 전역 컴포넌트: 플러그인, 라이브러리를 전역에서 사용할 때



### 컴포넌트와 인스턴스와의 관계

* 전역 컴포넌트는 모든 인스턴스에 등록이 되기 때문에 모든 인스턴스에서 사용 가능하다.
* 지역 컴포넌트는 각 인스턴스에 등록을 해야 사용할 수 있다.
* 보통 한 서비스에서 Vue 인스턴스는 하나이다.

# Reference

[Vue.js 시작하기 -Age of Vue.js](https://www.inflearn.com/course/Age-of-Vuejs/dashboard)

