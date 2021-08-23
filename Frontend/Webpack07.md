# Webpack - 최적화

**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 최적화

* 코드가 많아지면 번들링된 결과물이 메가바이트 단위로 커지게 되어, 브라우저 성능에 영향을 준다.
* 웹팩으로 번들 결과를 압축하거나 분리하여 최적화를 한다.



## 2. mode

* 웹팩의 mode 값을 설정



### development mode

* development는 디버깅 편의를 위해 두 개의 플러그인을 사용
  * NamedChunksPlugin
  * NamedModulesPlugin
* DefinePlugin을 사용시, process.env.NODE_ENV 값이 development로 설정되어 전역 변수로 주입됨



### production mode

* mode를 production으로 설정하면 JavaScript 결과물을 최소화하기 위해서 일곱 개 플러그인을 사용.
  * FlagDependencyUsagePlugin
  * FlagIncludeChunksPlugin
  * ModuleConcatenationPlugin
  * NoEmitOnErrorsPlugin
  * OccurrenceOrderPlugin
  * SideEffectsFlagPlugin
  * TerserPlugin: 기본 설정으로, JavaScript 코드를 난독화하고 debugger 구문을 제거
* DefinePlugin을 사용시, process.env.NODE_ENV 값이 production로 설정되어 전역 변수로 주입됨



### 환경 변수에 따른 mode 설정

* **webpack.config.js**에서 mode라는 상수를 아래와 같이 정의할 수 있다.
  * 환경변수에 따라서 모드를 설정 가능

```JavaScript
const mode = process.env.NODE_ENV || 'development';

module.exports = {
  mode,
}
```

* **package.json**에서 scripts를 설정
  * build 시에는 production mode
  * start 시에는 development mode

```json
...
"scripts": {
  "build": "NODE_ENV=production webpack --progress",
  "start": "webpack-dev-server --progress"
},
...
```



## 3. optimazation으로 최적화

* 빌드 과정을 커스터마이징



### optimize-css-assets-webpack-plugin

* css 파일 빈칸을 없애서 압축
  * **npm i -D optimize-css-assets-webpack-plugin** 을 입력하여 설치
  * webpack.config.js에 추가

```JavaScript
...
const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin');
// node의 모듈 시스템
module.exports = {
...
  optimization: {
    minimizer: mode === 'production' ? [
      new OptimizeCSSAssetsPlugin()
    ] : []
  },
 ...
}
```



### terser-webpack-plugin

* production일 경우 사용되는 플러그인 중 하나
* 기본 설정으로 JavaScript 코드를 난독화 하고 debugger 구문을 제거
* console.log를 제거하는 옵션도 있다.
* **npm i -D terser-webpack-plugin** 을 입력하여 설치
* webpack.config.js에 추가

```JavaScript
...
const TerserPlugin = require('terser-webpack-plugin');
// node의 모듈 시스템
module.exports = {
...
  optimization: {
    minimizer: mode === 'production' ? [
      new OptimizeCSSAssetsPlugin(),
      new TerserPlugin({
        terserOptions: {
          compress: {
            // console.log를 제거하는 옵션
            drop_console: true,
          }
        }
      })
    ] : []
  },
 ...
}
```



## 4. 코드 스플리팅

* 코드를 압축해도, 프로젝트가 커지면 브라우저 성능에 영향을 줄 수 있다.
* 결과물을 나누어 쪼개서 브라우저에서 다운로드 속도를 높인다.
  * 큰 파일 하나를 다운받는 것 보다 작은 파일 여러개를 동시에 다운받는 것이 빠르다.



### 엔트리 분리

* 엔트리를 여러개로 나누어 다운로드 속도를 높인다.
* 중복되는 코드를 제거해야한다.
  * **optimization**에 **splitChunks**를 추가
  * 중복되는 코드들은 **vendors-main-result.js**파일에 들어간다.

```JavaScript
...
// node의 모듈 시스템
module.exports = {
  ...
  optimization: {
   ...
    splitChunks: {
      // 중복되는 코드를 제거
      chunks: 'all'
    }
  },
 ...
}
```



### Dynamic Import

* 엔트리 분리 대신 dynamic import를 사용하여 자동으로 변경할 수 있다.
* 웹펙이 파일을 처리할 때 청크로 분리한다.

```JavaScript
// src/app.js
import axios from 'axios';
import './app.css';

document.addEventListener('DOMContentLoaded', async () => {
  // 페이지가 로딩되었을 때 api요청을 날린다.
  // 요청은 웹팩 개발서버로 날아감
  const res = await axios.get('/api/users');
  // 받은 응답을 html div안에 출력
  document.body.innerHTML = (res.data || []).map(user => {
    return `<div>${user.id}: ${user.name}</div>`
  }).join('');

  // result를 사용하는 부분
  // webpackChunkName이라는 주석을 보고 웹팩이 해당 부분을 따로 번들링한다.
  import(/* webpackChunkName: "result" */ './result.js').then(m => {
    // m: result 모듈
    const result = m.default;
    const resultEl = document.createElement("div");
    resultEl.innerHTML = await result.render();
    document.body.appendChild(resultEl);
  })
});
```



### externals

* 번들하지말아야할 대상은 빌드 범위에서 빼는 것
* 패키지들은 보통 빌드된 파일이 있다.
  * dist 폴더
* **copy-webpack-plugin**: 웹팩이 실행될 때 패키지 빌드 파일을 복사
  * **npm i -D copy-webpack-plugin**을 입력하여 설치
* webpack.config.js의 플러그인 추가

```JavaScript
...
const CopyPlugin = require('copy-webpack-plugin');
// node의 모듈 시스템
module.exports = {
 ...
  // 플러그인을 넣는 배열
  plugins: [
   ...
    new CopyPlugin([{
      // 어디에있는것을 복사하여 가져올지
      from: './node_modules/axios/dist/axios.min.js',
      to: './axios.min.js'
    }])
  ],
    externals: {
      // 웹팩으로 빌드시 axios 사용하는 부분이 있으면 전역변수 axios 사용하는 것으로 간주
      axios: 'axios'
    }
}
```

* html 파일에 패키지를 로딩하는 script태그 추가

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document<%= env %>
  </title>
</head>
<body>
  <!-- axios를 로딩 -->
  <script type="text/javascript" src="axios.min.js"></script>
</body>
</html>
```



## 5. 총정리

### Node.js/NPM

* 프로젝트를 생성하고 의존성을 해결



### Webpack

* 번들링
* 모듈을 사용하기 위한 도구
* 모듈로 작성한 프론트엔드 코드를 하나의 결과(번들)로 만듦
* API를 개발서버에 연동
* 핫로딩 설정
* 번들 결과 최적화



### Babel

* 최신 ECMAScript를 다루기 위한 도구
* 폴리필
* SASS/SCSS



### ESLint/Prettier

* 코드의 품질, 포매팅
* 두 도구를 함께 사용
* Lint를 자동화하고 강제화하는 것은 유용



> 다룬 개발도구의 역할과 **기본 개념을 확실히 기억**하고 자세한 것은 메뉴얼을 찾아본다. **기본 개념**을 잘 숙지한 상태에서 변화에 적응하는 **적응력**을 키워야만 빠르게 변화하는 프론트엔드 기술에 대처할 수 있다.



# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)

