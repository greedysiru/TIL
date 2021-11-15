# 웹팩 - plugin

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. plugin 적용

### plugin 설치

```shell
npm i -D mini-css-extract-plugin
```





### webapck.config.js

* 설치한 플러그인을 불러오기

```JavaScript
// webpack.config.js
var path = require('path');
// 플러그인 불러오기
var MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  mode: 'none',
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          // 플러그인의 로더
          { loader: MiniCssExtractPlugin.loader },
          "css-loader"
        ]
      }
    ]
  },
  // 플러그인 주요 속성
  plugins: [
    new MiniCssExtractPlugin()
  ],
}
```



## 2. plugin의 역할

* 웹팩의 기본적인 동작에 추가적인 기능을 제공하는 속성
* plugin 속성에는 배열의 형태로 생성자 함수로 생성한 객체 인스턴스만 추가 가능

```JavaScript
// webpack.confing.js
...
module.exports = {
  ...
  plugins: [
    new HtmlWebpackPlugin(),
    new webpack.ProgressPlugin()
  ]
}
```



### vs. loader

|        plgin         |            loader             |
| :------------------: | :---------------------------: |
| 결과물의 형태를 바꿈 | 해석하고 변환하는 과정에 관여 |



# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)

