# Babel - 바벨 사용법과 웹팩 통합

**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 프리셋 사용하기

* **preset-env**: ECMAScript2015+를 변환할 때 사용
  * **npm i @babel-env**를 입력하여 설치
* **preset-flow**
* **preset-react**
* **preset-typescript**:  TypeScript 코드를 ES5로 변환



## 2. 타겟 브라우저

* 프리셋을 사용할 때 특정 브라우저를 지정하여 지원하도록 할 수 있다.



### babel.config.js

```JavaScript
module.exports = {
  presets: [
    ['@babel/preset-env', {
      targets: {
        chrome: '79',
        ie: '11'
      }
    }]
  ]
}
```

* 이제 바벨이 코드를 크롬 79 버전과 IE 11버전을 지원하도록 트랜스파일할 것이다.



## 3. 폴리필

* Promise 객체의 경우 바벨이 변환하지 못한다.
  * ECMAScript5로 변환이 안되기 때문
* 바벨은 ECMAScript2015+를 ECMAScript5 버전으로 변환할 수 있는 것만 빌드한다.
* 변환할 수 없는 것들은 **폴리필**을 사용하여 해결
  * core-js
  * **npm i core-js**를 입력하여 설치



### bable.config.js

```JavaScript
module.exports = {
  presets: [
    ['@babel/preset-env', {
      targets: {
        chrome: '79',
        ie: '11'
      },
      // 폴리필 사용 방식 지정
      useBuiltIns: 'usage',
      // 폴리필 버전 지정
      corejs: {
        version: 2,
      }
    }]
  ]
}
```



## 4. 웹팩으로 통합

* 바벨을 웹팩의 로더 형식으로 적용하여 번들링한다.
  * babel-loader
  * npm i babel-loader



### webpack.config.js

```JavaScript
...
// node의 모듈 시스템
module.exports = {
...
  module: {
    rules: [
      ...
      , {
        // js 파일에 대해서 babel-loader 적용
        test: /\.js$/,
        loader: 'babel-loader',
        // node_moduels 아래의 js 파일은 제외
        exclude: /node_moduels/
      }
    ]
  },
  ...
```





# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)

