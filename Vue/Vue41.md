# Vue.js -  HOC

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. HOC

* High Order Component
  * **컴포넌트의 코드마저 재사용하는 기술**
  * React에서 기원



## 2. HOC 구현

### HOC 정의

* 정의한 HOC에 맞게 Vuex의 Action, Mutation 과 api를 만들 것
  * 해당 HOC는 route name을 dispatch로 보내서 해당하는 api를 호출하고 data를 mutation에 넘기도록 설계 됨

```JavaScript
// HOC 
import ListView from './ListView.vue';
import bus from '../utils/bus.js';

export default function createListView(name) {
  return { 
    // 재사용할 인스턴스(컴포넌트) 옵션들이 들어갈 자리
    name,
    created() {
    // 데이터를 요청
     // 스피너 이벤트 전송 (보내는 곳)
    bus.$emit('start:spinner');
    // dispatch가 되는 시점의 라우트 name을 보냄
    this.$store.dispatch('FETCH_LIST', this.$route.name)
    // 프로미스 체이닝
      .then(() => {
        bus.$emit('end:spinner');
      })
      .catch((error) => {
        console.log(error);
      });
    },
    // 컴포넌트를 로딩
    render(createElement) {
      return createElement(ListView);
    }
  }
}
```



### Route에 HOC 등록

```JavaScript
import Vue from 'vue';
import VueRouter from 'vue-router';
import UserView from '../views/UserView.vue';
import ItemView from '../views/ItemView.vue';
// HOC
import createListView from '../views/CreateListView.js';

Vue.use(VueRouter);

// Vue Router를 관리하는 객체
export const router = new VueRouter({
  mode: 'history',
  routes: [
    {
      path: '/',
      redirect: '/news',
    },
    {
      // path: url 주소
      path: '/news',
      name: 'news',
      // HOC
      component: createListView('NewsView'),
    },
    {
      path: '/ask',
      name: 'ask',
      // HOC
      component: createListView('AskView'),
    },
    {
      path: '/jobs',
      name: 'jobs',
      // HOC
      component: createListView('JobsView'),
    },
		...
  ]
})
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

