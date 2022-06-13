# Vue.js - Vue 테스트 유틸 라이브러리



## 1. Vue 테스트 유틸 라이브러리란

* Vue.js 공식 테스트 라이브러리
  * 유닛 테스트
* jest 만으로는 컴포넌트를 테스트하기위해 사용되어야 하는 코드가 많아짐
  * 테스트 유틸 라이브러리로 간단하게 뷰 컴포넌트를 테스트할 수 있음

### 예시

```JavaScript
// 특정 컴포넌트를 마운팅하는 API
import { shallowMount } from '@vue/test-utils';
// 이제 vue를 import하지 않아도 됨
// import Vue from 'vue';
import LoginForm from './LoginForm.vue';

// 컴포넌트의 이름이 테스트 최소 단위
describe('LoginForm.vue', () => {
  test('컴포넌트가 마운팅되면 usename이 존재하고 초기 값으로 설정되어 있어야 함', () => {
    // 컴포넌트 생성, 마운트
    // as-is const instance = new Vue(LoginForm).$mount();
    const wrapper = shallowMount(LoginForm);
    // 인스턴스가 username data가 초기값으로 되어 있는 지 확인
    expect(wrapper.vm.username).toBe('');
  });
});
```



## 2. 컴포넌트 HTML 요소 접근하기

* shallowMount API로 마운트된 인스턴스에 find 메서드로 특정 HTML 요소 접근 가능
  * 파라미터는 CSS 선택자

```JavaScript
 const idInput = wrapper.find('#username');
```



## 3. 마운트할 컴포넌트의 옵션 지정하기

* shallowMount: 첫 번째 파라미터로 전달 받은 컴포넌트를 마운트하는 API
  * 두 번째 파라미터는 마운트할 컴포넌트의 옵션(객체)

```JavaScript
const wrapper = shallowMount(LoginForm, {
  data() {
    return {
      // 컴포넌트의 username이 test
      username: 'test',
    };
  },
});
```



## 4. 사용자 관점의 테스트 코드 작성하기

* ID가 이메일이 아닌 경우, 경고 문구를 출력하는 컴포넌트
* 사용자 관점에서, ID를 이메일 형식이 아닌 것으로 입력했을 때 해당 경고 문구가 보여야함
  * 이 과정을 테스트로 구현
  * 올바르지 않은 값(ID) -> 경고 문구

```JavaScript
import { shallowMount } from '@vue/test-utils';
import LoginForm from './LoginForm.vue';

describe('LoginForm.vue', () => {
  test('ID가 이메일 형식이 아니면 경고 메시지가 출력된다.', () => {
    const wrapper = shallowMount(LoginForm, {
      data() {
        return {
          // 컴포넌트의 username이 test(이메일 형식이 아님)
          username: 'test',
        };
      },
    });
    // usename의 형식이 email이 아닐 때 경고하는 문구를 가져오기
    const waringText = wrapper.find('.warning');
    // username이 test이므로(이메일 형식이 아니므로) warningText가 있어야 함
    // exists() 해당 HTML 요소가 존재하는지 Boolean으로 return
    expect(waringText.exists()).toBeTruthy();
  });
});

```







## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

