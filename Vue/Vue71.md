# Vue.js - Jest

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. 테스트 코드 작성

* describe: 연관된 테스트 케이스를 그룹화
* test: 하나의 테스트를 실행
  * 첫 번째 파라미터 : 테스트 실행시 터미널에 표시할 문자열
  * 두 번째 파라미터 : 테스트를 실행할 콜백
* expect: 테스트할 값
  * toBe: 테스트할 값이 teBe에 전달할 값과 같은지 확인



### 예시

```JavaScript
// math.js
export function sum(a, b) {
  return a + b;
}
```

```JavaScript
// math.spec.js
// 테스트할 함수를 import
import { sum } from './math';

sum(10, 20); // 30이 나오는지 테스트

// 연관된 테스트 케이스를 그룹화하는 API
describe('math.js', () => {
  test('10 + 20 = 30', () => {
    const result = sum(10, 20);
    // 기대되는 값이 30일 것임
    expect(result).toBe(30);
  });
});

```



## 2. Jest 관련 설정

### ESLint

* 테스트 파일에서 ESLint Jest API들을 인식하지 못함
* .eslintrc.js에서 jest 관련 설정을 해줄 것

```JavaScript
module.exports = {
  root: true,
  env: {
    node: true,
    // jest 설정
    jest: true,
  },
  ...
};

```



## 3. Vue 컴포넌트 테스트

* 컴포넌트를 import하여, 인스턴스를 생성하여 테스트

```JavaScript
// Vue와 컴포넌트를 가져오기
import Vue from 'vue';
import LoginForm from './LoginForm.vue';

// 컴포넌트의 이름이 테스트 최소 단위
describe('LoginForm.vue', () => {
  test('컴포넌트가 마운팅되면 usename이 존재하고 초기 값으로 설정되어 있어야 함', () => {
    // 컴포넌트 생성, 마운트
    const instance = new Vue(LoginForm).$mount();

    // 컴포넌트의 username data가 초기값으로 되어 있는 지 확인
    expect(instance.username).toBe('');
  });
});

```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

