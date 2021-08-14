# Webpack - 엔트리와 아웃풋



**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. Webpack의 역할

* 모듈로 연결된 여러개의 JavaScript 파일을 묶어준다.
  * 이를 번들이라고 한다.
  * 즉, Webpack은 번들을 만드는 번들러라고 할 수 있다.



## 2. Webpack 설치

```shell
npm install -D webpack webpack-cli
```

* -D 옵션: devDependencies에 추가된다.
  * 개발용 패키지



## 3. Webpack 명령어

### 명령어 조회

```shell
node_modules/.bin/webpack --help
```



### --mode

* 아래의 세가지 값이 올 수 있다.
* development
  * 개발환경
* production
  * 운영환경
  * 배포하기위한 최적화 설정
* none



### --entry

* entry: 모듈의 시작점
* 모듈의 시작점을 지정



### --output-path

* 웹팩이 모듈을 합친 결과를 저장하는 경로



### --config

* 웹팩 설정 파일을 지정
* 기본명
  * webpack.config.js
  * webpackfile.js



## 4. 명령어 예시

```shell
node_moduels/.bin/webpack --mode development --entry ./src/app.js --output-path dist
```

* 개발환경에서
* 엔트리는 src/app.js로
* 모듈을 합친 결과는 dist 폴더에 main.js로 생성



## 5. webpack.config.js

```JavaScript
// node의 path 모듈
const path = require('path');
// node의 모듈 시스템
module.exports = {
  mode: 'development',
  entry: {
    main: './src/app.js',
  },
  // 두개의 인자가 필요
  output: {
    // 절대경로
    // node의 path 모듈
    path: path.resolve('./dist'),
    // 파일명
    // 엔트리에서 설정한 key 값
    // 동적으로 output을 만들기 위함
    filename: '[name].js'
  }
}
```



### npm 스크립트 설정 (package.json)

```json
{
...
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    // npm이 현재 프로젝트의 webpack을 찾아 실행
    // webpack은 기본 config 파일인 webpack.confing.js를 찾아 번들링 실행
    "build": "webpack"
  },
...
}
```

이후 `npm run build` 실행하면 번들링한다.

# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)