# Vue.js -  slot

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## slot

* 컴포넌트 내에 slot 태그를 정의
  * slot 태그 안은 비어있음
  * slot 태그 안의 내용은 상위 컴포넌트에서 정의
* 하위 컴포넌트에서 상위 컴포넌트로부터 정의될 영역에 slot태그를 넣고 name을 지정
* 상위 컴포넌트에서 하위 컴포넌트의 slot을 정의할 때 slot의 name에 맞게 적용
* **하위 컴포넌트를 부르는 페이지마다 데이터에 접근하는 속성이 다를 때 사용하면 유용**



### 예시

* 하위 컴포넌트
  * slot 태그 정의

```Vue
<template>
  <div class="user-container">
        <div class="fa-user">
        </div>
        <div class="user-description">
          <slot name="username">
            <!-- 상위 컴포넌트에서 정의할 영역 -->
            <!-- 미완성인 상태로 남겨놓고 상위 컴포넌트에서 정의 -->
          </slot>
          <div class="time">
            <slot name="time"></slot>
            <!-- 상위 컴포넌트에서 정의할 영역 -->
          </div>
          <slot name="karma"></slot>
        </div>
    </div>
</template>
...
```



* 상위 컴포넌트1
  * 하위 컴포넌트에서 사용할 slot 내부를 정의

```Vue
<template>
  <div>
    <user-profile>
      <div slot="username">{{ userInfo.id }}</div>
      <template slot="time">{{ userInfo.created }}</template>
      <div slot="karma">{{ userInfo.karma }}</div>
    </user-profile>
  </div>
</template>
...
```



* 상위 컴포넌트2
  * 상위 컴포넌트1과 데이터 접근이 다름
  * slot을 사용하면 이와 같이 데이터 접근이 달라도 동일한 하위 컴포넌트를 사용할 수 있음

```Vue
<template>
  <div>
    <section>
      <!-- 사용자 정보 -->
      <user-profile :info="fetchedItem">
        <!-- 하위 컴포넌트 정의 -->
        <div slot="username">{{ fetchedItem.user }}</div>
        <template slot="time">{{ fetchedItem.time_ago }}</template>
      </user-profile>
    </section>
    <section>
      <h2>{{ fetchedItem.title }}</h2>
    </section>
    <section>
      <!-- 질문 댓글 -->
      <div v-html="fetchedItem.content">
      </div>
    </section>
  </div>
</template>
...
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

