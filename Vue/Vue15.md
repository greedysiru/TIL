# Vue.js - Modal, Slot, Transition

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex 강의를 토대로 작성하였습니다.**



## 1. Modal Component

* Transition 효과
* text/x-template로 구현
  * 템플릿을 모듈화



## 2. Modal Component 모듈화

* 프로젝트 전반에서 모달을 사용할 수 있도록 모듈화
  * 재사용성
* 일반적으로 자주 사용하는 모듈은 **src/components/common**과 같은 경로에 정리



### 예시

```Vue
<!-- src/components/common -->
<template>
   <transition name="modal">
        <div class="modal-mask">
          <div class="modal-wrapper">
            <div class="modal-container">

              <div class="modal-header">
                <slot name="header">
                  default header
                </slot>
              </div>

              <div class="modal-body">
                <slot name="body">
                  default body
                </slot>
              </div>

              <div class="modal-footer">
                <slot name="footer">
                  default footer
                  <button class="modal-default-button" @click="$emit('close')">
                    OK
                  </button>
                </slot>
              </div>
            </div>
          </div>
        </div>
      </transition>
</template>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}
  
.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

</style>
```



## 3. Slot

* 한 컴포넌트에서 모듈을 불러왔을 때 slot 부분을 재정의할 수 있음
  * 일부 UI를 재사용
* 각 컴포넌트별로 불러온 모듈의 slot을 재정의하여 사용할 수 있음



### 예시

```vue
<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer">
      <i class="fas fa-plus addBtn" v-on:click="addTodo"></i>
    </span>
    <!-- Modal 적용 -->
    <Modal v-if="showModal" @close="showModal = false">
      <!-- slot 재정의 -->
      <h3 slot="header">
        경고!
        <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
      </h3>
      <span slot="body">아무것도 입력하지 않으셨습니다.</span>
    </Modal>
  </div>
</template>

<script>
// 모달 모듈 가져오기
import Modal from './common/Modal.vue';
export default {
  data: function() {
    return {
      newTodoItem: "",
      // 모달의 노출 여부
      showModal: false,
    }
  },
  methods: {
    addTodo: function() {
      if (this.newTodoItem !== ''){
      // 부모로 보냄
      this.$emit('addToDoItem', this.newTodoItem);
      this.clearInput();
      } else {
        // 모달 노출
        this.showModal = true;
      }
    },
    clearInput: function() {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal: Modal
  },
}
</script>

<style scoped>
...
</style>
```



## 4. Transition

* Vue에서 제공
* Vue의 문법으로 컴포넌트에 효과를 넣을 수 있음



### Transition Classes

* v-enter: 처음 이펙트 시작 상태
* v-enter-to: 시작되고 끝난 상태
* v-leave: 없어지기 시작하는 상태
* v-leave-to: 없어진 상태
* 이에 맞게 클래스 지정
* 일반적으로 v-enter와 v-leave-to를, v-enter-to와 v-leave를 같이 사용



### 문법

```
**<transition-group name="클래스명" tag="적용할 태그명">**
```

* name 속성에 list속성을 지정하면
  * list-enter, list-enter-to, list-leave, list-leave-to 클래스가 생성

### 예시

```Vue
<template>
  <div>
    <!-- 트랜지션 효과 -->
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
        <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)"></i>
        <!-- 조건부 class, true인 경우 해당 class를 적용 -->
        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  // props 받아오기
  props: ["propsdata"],
  methods: {
    removeTodo: function(todoItem, index) {
      this.$emit('removeItem', todoItem, index);
    },
    toggleComplete: function(todoItem, index) {
      this.$emit('toggleItem', todoItem, index);
    }
  }
}
</script>

<style scoped>
...
/* 리스트아이템 트랜지션 효과*/

.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
...
</style>
```


# Reference

[Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/dashboard)

