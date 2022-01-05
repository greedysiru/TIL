# Vue.js -  데이터 흐름 처리

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. props

### 부모 컴포넌트

```Vue
<template>
  <div>
    <UserProfile></UserProfile>
  </div>
</template>

<script>
import UserProfile from '../components/UserProfile.vue';
export default {
  components: {
    UserProfile,
  },
  computed: {
    userInfo() {
      return this.$store.state.user;
    }
  },
  created() {
    const {userName} = this.$route.params;
    // action 호출 시 userName 전달(payLoad);
    this.$store.dispatch('FETCH_USER', userName);
  },
}
</script>
...
```



### 자식 컴포넌트

```Vue
<template>
  <div class="user-container">
        <div class="fa-user">
          user
        </div>
        <div class="user-description">
          <div>{{ info.id }}</div>
          <div class="time">
            {{ info.created }}
          </div>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    info: Object,
  },
}
</script>
...
```



## 2. 자식 컴포넌트에서 바로 접근

### 부모 컴포넌트

```Vue
<template>
  <div>
    <UserProfile></UserProfile>
  </div>
</template>

<script>
import UserProfile from '../components/UserProfile.vue';
export default {
  components: {
    UserProfile,
  },
  created() {
    const {userName} = this.$route.params;
    // action 호출 시 userName 전달(payLoad);
    this.$store.dispatch('FETCH_USER', userName);
  },
}
</script>
...
```



### 자식 컴포넌트

```Vue
<template>
  <div class="user-container">
        <div class="fa-user">
          user
        </div>
        <div class="user-description">
          <div>
        			{{ userInfo.id }}    
				  </div>
          <div class="time">
            {{ userInfo.created }}
          </div>
        </div>
    </div>
</template>

<script>
export default {
  computed: {
    userInfo() {
      return this.$store.state.user;
    }
  },
}
</script>
...
```



## 3. 2가지 데이터 처리 흐름 비교

* props
  * 컴포넌트 간의 데이터 흐름을 명시적으로 함
* 자식 컴포넌트에서 바로 접근
  * vuex의 의도에 맞게 사용
  * state를 어디서든 접근 가능한 이점을 활용
* 둘 다 틀린 방식이 아니므로 상황에 맞게 적절하게 사용

# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)