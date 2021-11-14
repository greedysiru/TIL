# 웹팩 - loader

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. webpack.config.js 분석

* mode
  * 세 가지 모드 지원(production, development, none)
  * 배포시에는 production으로 할 것
* entry: 웹팩으로 번들링할 파일의 주소(시작점)
* output: 결과물의 이름과 경로
* module: loader
  * rules 속성 안에 로더를 설정

```JavaScript
var path = require('path');

module.exports = {
  mode: 'none', // production, development, none
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        // 로더 대상 지정
        test: /\.css$/,
        // 웹팩으로 변활할 때 사용할 로더 지정
        use: ['style-loader', 'css-loader']
      },
      {
        test: /\.js$/,
        use: ['bable-loader']
      }
    ]
  },
}
```



## 2. loader

* 로더 없이 css와 같은 파일을 번들링할 수 없음
  * 에러 발생
* 적절한 로더를 추가해야 함
* css의 경우 두 개의 로더가 필요
* 로더는 오른쪽에서 왼쪽 순서로 적용 됨



### css-loader

* css를 인식할 수 있게 함



### style-loader

* css-loader에 앞서서 지정해야 함
* head 태그 안에 inline style로 css 코드를 넣어 줌



### sass를 사용하는 경우

* sass부터 처리를 해야하므로 아래와 같은 순서로 로더 지정

```JavaScript
...
    rules: [
      {
        // 로더 대상 지정
        test: /\.scss$/,
        // 웹팩으로 변활할 때 사용할 로더 지정
        use: ['style-loader', 'css-loader', 'sass-loader']
      },
...
```



# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)