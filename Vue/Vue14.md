# Vue.js - 컨테이너와 프레젠터, v-bind, v-on, 안티패턴

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. 컨테이너와 프레젠터

* 컨테이너: 비즈니스 로직(데이터 조작)
* 프레젠터: 데이터 표현
* 실질적인 데이터 조작을 상위 컴포넌트인 컨테이너에서 하고 그 아래의 프레젠터에서는 화면을 구현
  * 프레젠터 컴포넌트에서 이벤트를 감지하여 상위 컴포넌트로 전달
  * 상위 컴포넌트는 전달받은 이벤트에 따라 데이터 조작



## 2. v-bind

* 상위 컴포넌트로부터 하위 컴포넌트로 props를 넘길 수 있음

> **v-bind:내려보낼 프롭스 속성 이름 = "현재 위치의 컴포넌트 데이터 속성"**



### 예시

* 상위 컴포넌트

```Vue
<template>
  <div id="app">
    ...
    <TodoList v-bind:propsdata="todoItems"></TodoList>
    ...
  </div>
</template>

<script>
...
export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  created: function() 
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
      }
    }
  },
 ...
```



* 하위 컴포넌트

```Vue
...
<script>
export default {
  // props 받아오기
  props: ["propsdata"],
  ...
</script>
...
```



## 3. v-on

* 하위 컴포넌트에서 이벤트가 발생하면, 부모 컴포넌트로 해당 이벤트 발생과 인자를 넘길 수 있음
* 부모 컴포넌트에서 하위 컴포넌트의 이벤트를 감지하여 특정 메서드를 실행



### $emit

* 이벤트 이름과 인자들을 부모 컴포넌트로 보냄

> **this.$emit('이벤트이름', 인자1, 인자2, ...)**



### v-on

* 하위 컴포넌트에서 보낸 이벤트를 감지하여 부모 컴포넌트에 정의된 메서드를 사용

> **v-on:하위 컴포넌트에서 발생시킨 이벤트 이름 ="현재 컴포넌트의 메서드 명"**



### 예시

* 상위 컴포넌트

```Vue
<template>
...
    <TodoInput v-on:addToDoItem="addOneItem"></TodoInput>
...
</template>

<script>
...
  methods: {
    addOneItem: function(todoItem) {
      let obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    }
  },
...
</script>
...
```



* 하위 컴포넌트

```Vue
<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer">
      <i class="fas fa-plus addBtn" v-on:click="addTodo"></i>
    </span>
  </div>
</template>

<script>
...
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== ''){
      // 부모로 보냄
      this.$emit('addToDoItem', this.newTodoItem);
      this.clearInput();
      }
    },
    clearInput: function() {
      this.newTodoItem = '';
    }
  },
}
</script>
...
```



## 4. 안티패턴

>  **상위 컴포넌트의 데이터를 하위 컴포넌트로 전달한 후 하위 컴포넌트에서 변경하지 않아야 한다**

* 컨테이너의 데이터 조작을 프레젠터에서 하지 않도록 주의




# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

