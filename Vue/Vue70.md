# Vue.js - 테스팅,  Jest

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 테스팅이란

* 기능이 잘 동작하는지에 대해 검증
  * 테스트 코드는 작성해놓으면 자동으로 기능을 검증해줌
* 주로 유닛단위로 테스트



## Jest

* 자바스크립트 테스트 프레임워크
* 사용성이 좋고 문서화가 잘 되어있음
* React.js, Vue.js, Agular에서 사용 가능



### jest.config.js

* jest 설정 파일
* 테스트 파일을 지정할 수 있음(testMatch 속성)
* testMatch 속성이 없는 경우 test/unit 디렉토리 아래에 테스트를 만들어야 함
* test 파일은 가능하면 관련 파일과 근접해 있는 것이 좋음

```JavaScript
module.exports = {
  preset: '@vue/cli-plugin-unit-jest',
  // test를 실행할 파일
  testMatch: [
    '<rootDir>/src/**/*.spec.(js|jsx|ts|tsx)|**/__tests__/*.(js|jsx|ts|tsx)',
    // Example.spec.js 또는 Example.test.js 이면 테스트 파일로 인식
  ],
};
```



### scripts 설정

* package.json의 scripts 객체에 test 전용 스크립트 지정하기
* --watchAll 옵션 : 워크스페이스 내에서 수정사항이 발생하면 테스트 자동 실행

```json
...
"scripts": {
    "test": "vue-cli-service test:unit --watchAll",
	  ...
  },
...
```





## Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)

