# 웹팩 시작하기

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. 웹팩 소개

* 모듈 번들러(**Module Bundler**)
  * 웹 애플리케이션을 구성하는 자원(HTML, CSS, JavaScript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구
* 모듈 번들링
  * 웹 애플리케이션을 구성하는 몇십, 몇백개의 자원들을 하나의 파일로 병합 및 압축해주는 동작
* **빌드 == 번들링 == 변환**



## 2. 웹팩 설치 및 실행

### 웹팩 설치

```shell
npm i webpack webpack-cli -D
```



### 커스텀 명령어 추가

* package.json에 커스텀 명령어 추가

```json
...
"scripts": {
    "build": "webpack"
  },
...
```



### 커스텀 명령어 실행

```shell
npm run build
```



## 3. 웹팩 mode 적용

### mode

* development
* production
* none



### mode 적용

```json
...
"scripts": {
    "build": "webpack --mode=none"
  },
...
```



## 4. 웹팩 설정 파일

### webpack.config.js

* 프로젝트 루트 레벨에 생성
* 웹펙 명령어의 옵션 입력하는 대신 파일에 정의 가능

```JavaScript
// node.js의 common.js path모듈
var path = require('path');

module.exports = {
  mode: 'none',
  entry: './src/index.js',
  // 번들링 결과
  output: {
    // 파일 이름
    filename: 'main.js',
    // 경로
    path: path.resolve(__dirname, 'dist')
  }
};
```



## 5. 웹팩 변환 전후 결과 비교

* request 요청이 줄음
* 여러가지 파일을 하나로 합침
* 페이지 로딩 속도가 빨라짐



### 웹팩 빌드 결과

* 웹팩은 각 모듈을 번호로 관리
* IIFE안에 웹팩이 담겨 있음
  * **IIFE(Immediately Invoked Function Expression, 즉시 실행 함수)**

# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)

