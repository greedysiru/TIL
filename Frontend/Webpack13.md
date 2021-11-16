# 웹팩 - Webpack Dev Server

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. Webpack Dev Server가 필요한 이유

* 개발을 진행하면서, 코드의 결과를 실시간으로 확인 가능
* 웹 애플리케이션을 개발하는 과정에서 유용하게 사용되는 도구
* 웹팩의 빌드 대상 파일이 변경되었을 때 코드만 변경하고 저장하면 웹팩으로 빌드하여 브라우저를 새로고침
* 명령어 입력 시간, 브라우저 새로고침 시간, 웹팩 빌드 시간을 절약할 수 있음



## 2. Webpack Dev Server 설치 및 적용



### 설치

```shell
npm i webpack webpack-cli webpack-dev-server -D
```





### 명령어

```json
// package.json
...
"scripts": {
  "dev": "webpack-dev-server",
  "build": "webpack"
}
```



### webpack.config.js

```JavaScript
var path = require('path');
var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  mode: 'none',
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  devServer: {
    // Webpack Dev Server의 포트
    port: 9000,
  },
  plugins: [
    new HtmlWebpackPlugin({
      // index.html 템플릿을 기반으로 빌드 결과물을 추가해줌
      template: 'index.html',
    }),
  ],
};
```



## 3. Webpack Dev Server 특징

* 빌드 결과물이 파일 탐색기 또는 프로젝트 폴더에서 보이지 않음
* 컴퓨터 구조 관점에서 파일 입출력보다 메모리 입출력이 더 빠르고 컴퓨터 자원이 덜 소모



## 4. Proxy

* devServer의 속성 중 하나
* 개발 시에 CORS(Cross-Origin Resource Sharing) 방지
* 브라우저에서 벗어나 서버에서 서버로 요청



```JavaScript
module.exports = {
  devServer: {
    proxy: {
      '/api': 'domain.com'
    }
  }
};
```



# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)

