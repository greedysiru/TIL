# Vue.js - 로컬스토리지, 스타일 바인딩

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. 로컬스토리지에 객체 저장하고 사용하기

### JSON.stringify()

* JavaScript 값이나 객체를 JSON 문자열로 변환하는 API
* 로컬스토리지에 value를 넣기 위해서는 문자열로 변환해야 함
* 문자열화를 하지 않으면 JavaScript의 객체의 경우 [object Object]라는 값으로 저장 됨

```vue
<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer">
      <i class="fas fa-plus addBtn" v-on:click="addTodo"></i>
    </span>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      newTodoItem: ""
    }
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== ''){
      let obj = {completed: false, item: this.newTodoItem};
      // 로컬스토리지에 넣기 위해 문자열로 변환
      localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
      this.clearInput();
      }
    },
    clearInput: function() {
      this.newTodoItem = '';
    }
  },
}
</script>

<style scoped>
  ...
</style>
```



### JSON.parse()

* JSON 문자열의 구문을 분석하고, 그 결과에서 JavaScript 값이나 객체를 생성하는 API
* 로컬스토리지에 저장한 문자열화된 객체를 가져와서 다시 사용하기 위해서는 JavaScript 객체로 변환해야 한다.
  * 값이 문자열화 되어있어 프로퍼티 접근이 되지 않음

```vue
<template>
  ...
</template>
<script>
...
created: function() {
    // 로컬스토리지에 데이터가 있으면
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
          // 로컬스토리지의 key를 이용하여 value를 가져옴
          // 로컬스토리지에 저장된 값은 string이므로 JavaScript에 맞는 적절한 형태로 변환하기 위해 JSON.parse() API 사용
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
      }
    }
  },
...
</script>
```



## 2. 스타일 바인딩

* v-bind를 사용하여 조건부로 css 클래스를 지정할 수 있음
  * boolean이 true이면 해당  css 클래스가 적용



### 예시

```vue
<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
        <!-- todoItem.completed가 true이면 checkBtnCompleted 클래스가 적용 -->
        <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}"
           v-on:click="toggleComplete(todoItem, index)"></i>
        <!-- todoItem.completed가 true이면 textCompleted 클래스가 적용 -->
=        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
...
</script>

<style scoped>
...
</style>
```




# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

