# Vue.js -  공통 컴포넌트 구현(2) - computed, tempalte와 v-if

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. computed 속성

* computed는 미리 계산된 속성
* 계산된 속성은 캐시 되며 의존하고 있는 반응형 속성이 변경되는 경우 다시 평가 됨



### 예시

```Vue
<template>
  <div>
    <ul class="news-list">
      <!-- computed -->
      <li v-for="item in listItems" class="post">
        <!-- 포인트 영역 -->
        <div class="points">
          {{ item.points || 0}}
        </div>
        <!-- 기타 정보 영역 -->
        <div>
          <p class="news-title">
            <a :href="item.url">
              {{ item.title }}
            </a>
          </p>
          <small class="link-text">
              {{ item.time_ago }} by &nbsp;
              <!-- user 이동할 때 item.user에 대한 정보도 넘김 -->
              <router-link v-bind:to="`/user/${item.user}`" class="link-text">{{ item.user }}</router-link>
          </small>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  ...
  computed: {
    listItems() {
      // 라우트 name 속성을 가져오기
      const name = this.$route.name;
      // name에 맞는 state 가져오기
      if (name === 'news') {
        return this.$store.state.news;
      } else if (name === 'ask') {
        return this.$store.state.ask;
      } else if (name === 'jobs') {
        return this.$store.state.jobs;
      } 
    }
  }
}
</script>

...
```



## 2. tempalte와 v-if를 응용한 분기

* tempalte
  * 가상의 태그
  * 내부적으로 분기처리하여 해당하는 조건이면 렌더링
* v-if
  * 페이지에 맞는 분기처리를 할 수 있는 디렉티브



### 예시

```vue
<template>
  <div>
  		...
          <!-- 타이틀 영역 -->
          <p class="news-title">
            <!-- 내부적으로 분기처리하여 v-if에 해당하는 조건이면 렌더링 -->
            <template v-if="item.domain">
              <a :href="item.url">
                {{ item.title }}
              </a>
            </template>
            <template v-else>
              <router-link v-bind:to="`${item.url}`">
                {{ item.title }}
              </router-link>
            </template>
          </p>
			...
  </div>
</template>
...
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)