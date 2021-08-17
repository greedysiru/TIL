# Webpack - 플러그인(Plugin)



**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 플러그인의 역할

* 번들된 결과물 하나를 처리한다.
* 로더는 모듈로 연결된 각 파일을 처리
* 플러그인은 output으로 만들어질 번들링에 후처리
* JavaScript를 난독화 또는 특정 텍스트를 추출하는 용도로 사용



## 2. 커스텀 플러그인 만들기

### 플러그인 클래스 정의

```JavaScript
// my-webpack-plugin.js
class MyWebpackPlugin {
  // 플러그인 메소드
  // compiler라는 객체를 주입
  apply(compiler) {
    // 플러그인이 완료되었을 때 콜백함수를 실행
    compiler.hooks.done.tap('My Plugin', stats => {
      console.log('MyPlugin: done');
    })
  }
}

module.exports = MyWebpackPlugin;
```



### webpack.config.js

```JavaScript
...
// 플러그인 가져오기
const MyWebpackPlugin = require('./my-webpack-plugin');
// node의 모듈 시스템
module.exports = {
  ...
  // 플러그인을 넣는 배열
  plugins: [
    new MyWebpackPlugin(),
  ]
}
```



## 3. 번들된 결과 처리하기

### BannerPlugin

```JavaScript
const { Compilation } = require("webpack");

class MyWebpackPlugin {
  // 플러그인 메소드
  // compiler라는 객체를 주입
  apply(compiler) {
    compiler.plugin('emit', (compilation, callback) => {
      // complilation 객체를 이용해서 웹팩이 번들링한 결과물에 접근
      const source = compilation.assets['main.js'].source();
      // 번들 결과물에 내용 추가
      compilation.assets['main.js'].source = () => {
        // 배너를 만들고 원본 source와 합하여 반환
        const banner = [
          '/**',
          ' * 이것은 BannerPlugin이 처리한 결과입니다.',
          ' * Build Date: 2021-08-15',
          ' */'
        ].join('\n');
        return banner + '\n\n' + source;
      }

      callback();
    })
  }
}

module.exports = MyWebpackPlugin;
```



## 4. 자주 사용하는 플러그인

### BannerPlugin

* 빌드한 결과물에 빌드 정보, 커밋 정보를 추가
* Webpack이 기본적으로 제공하는 플러그인
* 빌드 후 배포했을 때 정적 파일이 잘 적용되고 캐시에 의해 갱신이 안되지 않는지 확인할 수 있음
* **webpack.config.js**에서 설정

```JavaScript
const path = require('path');
// 플러그인 가져오기
const webpack = require('webpack');
// 터미널 명령을 실행할 수 있는 노드 모듈
const childProcess = require('child_process');
// node의 모듈 시스템
module.exports = {
  ...
  // 플러그인을 넣는 배열
  plugins: [
    new webpack.BannerPlugin({
      banner: `
      Build Date: ${new Date().toLocaleString()}
      Commit Version: ${childProcess.execSync('git rev-parse --short HEAD')}
      Author: ${childProcess.execSync('git config user.name')}
      `
    })
  ]
}
```



### DefinePlugin

* 프론트엔드 소스코드는 개발환경과 운영환경으로 나누어서 관리
  * 환경에 따라서 API 서버 주소가 다를 수 있음
  * 같은 소스 코드를 두 환경에 배포하기 위해서는 환경 의존적인 정보를 소스가 아닌 곳에서 관리
* 웹팩에서 기본적으로 제공하는 플러그인
* 플러그인에 빈 객체를 전달해도 기본적으로 넣어주는 값이 있다.
  * 노드 환경 정보인 process.env.NODE_ENV
  * 웹팩 설정의 mode에 설정한 값이 여기에 들어감(development)
* 플러그인에 객체를 전달하면, 해당 key는 전역변수로 접근 가능
* **webpack.config.js**에서 설정

```JavaScript
const path = require('path');
// 플러그인 가져오기
const webpack = require('webpack');
...
// node의 모듈 시스템
module.exports = {
...
  // 플러그인을 넣는 배열
  plugins: [
...
    new webpack.DefinePlugin({
      // 어플리케이션에서 TWO라는 전역변수로 접근 가능
      TWO: JSON.stringify('1+1'),
      // 어플리케이션에서 api.domain이라는 전역변수로 접근 가능
      'api.domain': JSON.stringify('http://dev.api.domain.com')
    })
  ]
}
```



### HtmlTemplatePlugin

* 3rd party package
* HTML 파일을 처리할 때 사용
* **npm i -D html-webpack-plugin**을 입력하여 설치
* 빌드 과정에 html을 포함
* 유동적으로 템플릿을 만들 수 있음



### HTMLTemplatePlugin 예시

* **webpack.config.js**

```JavaScript
...
const HtmlWebpackPlugin = require('html-webpack-plugin');
// node의 모듈 시스템
module.exports = {
 ...
  // 플러그인을 넣는 배열
  plugins: [
    ...
    new HtmlWebpackPlugin({
      // template 경로 전달
      template: './src/index.html',
      templateParameters: {
        env: process.env.NODE_ENV === 'development' ? '(개발용)' : ''
      },
      // 운영환경일 때만 실시
      minify: process.env.NODE_ENV === 'production' ? {
        // 빈칸 제거
        collapseWhitespace: true,
        // 주석 제거
        removeComments: true,
      } : false
    })
  ]
}
```

* **src/index.html**

```HTML
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <-- ejs문법, 웹팩으로부터 변수를 넘겨받을 수 있음 -->
  <title>Document<%= env %>
  </title>
</head>

<body>
</body>

</html>
```



### CleanWebpackPlugin

* 3rd party package
* output 폴더를 삭제
  * 빌드할때마다 삭제
* **npm i -D clean-webpack-plugin**을 입력하여 설치
* 이후, **webpack.config.js**의  plugins 배열에 추가



### MiniCssExtractPlugin

* 3rd party package
* 스타일시트가 점점 많아지면 하나의 JavaScript 결과물로 만드는 것이 부담
* 번들 결과에서 스타일시트 코드만 뽑아, 별도의 CSS 파일로 만들어 역할에 따라 파일을 분리하는 것이 좋음
  * JavaScript파일 하나, CSS파일 하나
* 브라우저에서 큰 파일 하나를 내려받는 것보다, 여러 개의 작은 파일을 동시에 다운로드하는 것이 빠르기 때문
  * 프로덕션 환경에서는 분리하는 것이 효과적
* CSS를 별도 파일로 뽑아내는 플러그인
* **npm i -D mini-css-extract-plugin**을 입력하여 설치
* **webpack.confing.js**에 설정 추가

```JavaScript
...
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
// node의 모듈 시스템
module.exports = {
...
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          // 운영환경일 때만 MiniCssExtractPlugin의 로더 실행
          process.env.NODE_ENV === 'production'
            ? MiniCssExtractPlugin.loader
            : 'style-loader',
          'css-loader'
        ]
      },
     ...
  // 플러그인을 넣는 배열
  plugins: [
    ...
    // 운영환경에서만 실행
    ...(process.env.NODE_ENV === 'production'
      ? [new MiniCssExtractPlugin({ filename: '[name].css' })]
      : []
    )
  ]
}
```





# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)