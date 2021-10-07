# Vue.js - 컴포넌트 생성, 반응형 태그, scoped, v-model, v-on, v-for

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. 컴포넌트 생성 및 등록

### 컴포넌트 생성

* 보통 src/components에 컴포넌트를 생성
* 컴포넌트 이름은 pascal case
* Vetur이 있으면, vue를 입력하면 싱글 파일 컴포넌트 생성

```Vue
<!-- vue 단축키, 싱글 파일 컴포넌트 생성 -->
<template>
  <!-- html -->
  <!-- 템플릿 안의 HTML 태그는 하나 -->
</template>

<script>
export default {
  // JS Script
}
</script>

<style>
  /* CSS */
</style>
```



### 컴포넌트 등록

* src/App.vue에 생성한 컴포넌트들 등록

```Vue
<template>
  <div id="app">
    <!-- 케밥 케이스가 권장되지만 파스칼케이스로도 사용 가능 -->
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
    <TodoList></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
// 각각의 파일 내용을 담아옴
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  name: 'App',
  components: {
    // 컴포넌트 태그명 : 컴포넌트 내용
     'TodoHeader' : TodoHeader,
     "TodoInput" : TodoInput,
     "TodoList" : TodoList,
     "TodoFooter" : TodoFooter,
  }
}
</script>

<style>

</style>

```



## 2. 반응형 태그 설정

### 반응형 태그

* 뷰포트 메타 태그
* **width=device-width**
  * 뷰포트의 너비를 기기의 너비로 설정
* 반응형 웹
  * 어떤 기기에서라도 해당 기기에 최적화된 화면을 보여주는 것

```HTML
<head>
  ...
  <meta name="viewprot" content="width=device-width, initial-scale=1">
</head>
```



## 3. scoped

* 해당 컴포넌트에서만 제한되는 CSS 규칙을 추가할 때 사용

```vue
<template>
  <header>
    <h1>TODO it!</h1>
  </header>
</template>
<style scoped>
  h1 {
    color: #2F3B52;
    font-weight: 900;
    margin: 2.5rem 0 1.5rem;
  }
</style>
```



## 4. v-model, v-on

### v-model

* **양방향 바인드**를 하는 디렉티브
* DOM 요소에 입력되는 데이터와 Vue 인스턴스를 동적으로 매핑
  * 화면의 데이터 변경과 Vue 인스턴스 안의 데이터 변경이 동기화
  * ex) input에 입력된 데이터가 Vue 인스턴스에서 접근이 가능하게 되거나 Vue 인스턴스에서 조작한 데이터를 input에서 표시



### v-on

* 이벤트를 감지하여 메소드를 실행시키는 디렉티브
  * ex) onClick 이벤트를 감지하여 특정 메소드를 실행



### 예시

```Vue
<template>
  <div>
    <!-- input에 입력된 텍스트 값을 동적으로 Vue 인스턴스에 매핑 -->
    <input type="text" v-model="newTodoItem">
    <!-- 클릭시 addTodo 메소드 실행 -->
    <button v-on:click="addTodo">add</button>
  </div>
</template>
<script>
export default {
  data: function() {
    // v-model 디렉티브에의해 input에 입력되는 값이 동적으로 매핑
    // 화면에서의 데이터 변경과 Vue 인스턴스 안의 데이터 변경이 동기화
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function() {
      // 컴포넌트의 newTodoItem 접근
      console.log(this.newTodoItem);
      // 저장하는 로직
      localStorage.setItem(this.newTodoItem, this.newTodoItem);
      // 초기화
      this.newTodoItem = '';
    }
  }
}
</script>
...
```



## 5. v-for

* 배열을 순회하여 접근해서 각 요소를 DOM으로 렌더링할 수 있는 디렉티브
* v-for 사용시 v-bind:key를 지정해야 함
  * DOM 노드들을 추적하고 기존 엘리먼트를 재사용/정렬하기 위해



### 예시

```Vue
<template>
  <div>
    <ul>
      <!-- v-for 사용시 v-bind:key를 지정해야함 -->
      <!-- v-for가 순회하며 todoItems의 요소들을 하나씩 찍어냄 -->
      <li v-for="todoItem in todoItems" v-bind:key="todoItem">
        {{ todoItem }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  // Vue 라이프 사이클
  // 인스턴스가 생성되자마자 호출되는 라이프사이클 훅
  created: function() {
    // 로컬스토리지에 데이터가 있으면
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
          // 로컬스토리지에 있는 요소들을 집어 넣음
          this.todoItems.push(localStorage.key(i));
      }
    }
  }
}
</script>
...
```




# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

