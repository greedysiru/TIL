# Babel - 기본개념(등장 배경, 설치, 기본 동작, 플러그인)

**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 등장 배경

### 크로스 브라우징

* 브라우져마다 사용하는 JavaScript 언어가 조금씩 다르다.
  * IE는 프로미스를 이해하지 못한다.
  * 크로스 브라우징 이슈
* 바벨이 크로스 브라우징 이슈를 해결
  * ECMAScript2015+로 작성한 코드를 모든 브라우져에서 동작하도록 호환성을 보장
  * TypeScript, JSX 포함



## 2. 설치 및 기본 동작

### 설치

```shell
npm install @babel/core @babel/cli
```



### 실행

```shell
npx babel app.js
```



### 기본 동작

* 세 단계로 빌드 진행
* **파싱(Parsing)**: 코드를 각 토큰별로 분해
  * const, alert, 등호 등등으로 분해
* **변환(Transforming)**: ES6 -> ES5로 변환
  * 플러그인이 담당
* **출력(Printing)**



## 3. 플러그인

* 변환(Transforming)을 담당



### 커스텀 플러그인 예시 1

```JavaScript
module.exports = function myBabelPlugin() {
  return {
    // 커스텀 바벨 플러그인은 visitor라는 객체를 반환
    visitor: {
      // parsing된 결과인 path라는 객체를 받음
      Identifier(path) {
        // 파싱된 결과물에 접근
        const name = path.node.name;

        // 바벨이 만든 AST 노드를 출력
        console.log('Identifier() name:', name)

        // 변환작업: 코드 문자열을 역순으로 변환
        // 파싱되어진 토큰들이 역순으로 뒤집어짐
        path.node.name = name
          .split("")
          .reverse()
          .join("");
      }
    },
  };
}
```

이후, npx로 babel을 플러그인을 적용하여 실행

```shell
npx babel app.js --plugins './my-babel-plugin.js'
```



### 커스텀 플러그인 예시 2

```JavaScript
module.exports = function myBabelPlugin() {
  return {
    // 커스텀 바벨 플러그인은 visitor라는 객체를 반환
    visitor: {
      VariableDeclaration(path) {
        console.log('VariableDeclaration() kind:', path.node.kind); // const
        // const => var 변환
        if (path.node.kind === 'const') {
          path.node.kind = 'var'
        }
      },
    },
  };
}
```



### block-scoping 플러그인

* const, let 처럼 블록 스코핑을 사용하는 예약어를 함수 스코핑을 사용하는 var로 변환
* **npm i -D @babel/plugin-transform-block-scoping**을 입력하여 설치
* 아래를 입력하여 실행

```shell
npx babel app.js --plugins @babel/plugin-transform-block-scoping
```



### arrow-functions 플러그인

* 화살표 함수를 일반 함수로 변환
* **npm i -D @babel/plugin-transform-arrow-functions**을 입력하여 설치
* 아래를 입력하여 실행

```shell
npx babel app.js --plugins @babel/plugin-transform-arrow-functions
```



### strict-mode 플러그인

* ECMAScript5에서부터 지원하는 엄격모드를 사용하는 것이 안전
  * **use strict** 구문
* **npm i -D @babel/plugin-transform-strict-mode**를 입력하여 설치
* 아래를 입력하여 실행

```Shell
npx babel app.js --plugins @babel/plugin-transform-strict-mode
```



## 4. babel.config.js

* 바벨 설정 파일
  * **npx babel app.js** 를 입력하면 babel.config.js를 기반으로 플러그인을 실행

```JavaScript
module.exports = {
  plugins: [
    "@babel/plugin-transform-block-scoping",
    "@babel/plugin-transform-arrow-functions",
    "@babel/plugin-transform-strict-mode",
  ]
}
```



## 5. 프리셋

* 필요한 플러그인을 하나하나 설정하는 것은 비효율 적임
* 목적에 맞게 여러가지 플러그인을 세트로 묶어놓은 것을 **프리셋**이라 함



### 커스텀 프리셋

```JavaScript
// my-babel-preset.js
module.exports = function myBabelPreset() {
  return {
    plugins: [
      "@babel/plugin-transform-block-scoping",
      "@babel/plugin-transform-arrow-functions",
      "@babel/plugin-transform-strict-mode",
    ]
  }
}
```

```JavaScript
// babel.config.js
module.exports = {
  presets: [
    './my-babel-preset.js'
  ]
}
```





# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)