

# Vue.js - ESLint & Prettier

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. ESLint

* 런타임에 오류가 발생하지 않도록 설정한 규칙에 따라 JavaScript 문법의 문제 패턴을 교정해주는 정적 코드 분석 도구



### .eslintrc.js

* ESLint의 설정 파일
* rules를 지정하여 프로젝트의 JavaScript 코드를 이에 따라 검사



## 2. Prettier

* 코드 정리 도구
* 코드의 한줄 길이, 세미콜론, 따옴표 등의 기준을 정할 수 있음
* .prettierrc : 프리티어 설정 파일
  * **ESLint와 병용하는 경우 충돌이 되지 않도록 .eslintrc.js에서 프리티어를 설정할 것**



### 3. ESLint에 Prettier 규칙 적용

* ESLint와 Prettier를 병용하여 일관된 코드를 작성할 수 있도록 함



### 규칙 적용 예시

* .eslintrc.js의 rules객체에 prettier를 적용
* prettier/prettier 라는 key로 등록
  * value는 배열

```JavaScript
module.exports = {
 ...
  rules: {
    "prettier/prettier": ['error', {
        singleQuote: true,
        semi: true,
        useTabs: true,
        tabWidth: 2,
        trailingComma: 'all',
        printWidth: 80,
        bracketSpacing: true,
        arrowParens: 'avoid',
      },]
  },
...
};

```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)