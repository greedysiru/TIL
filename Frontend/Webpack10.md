# 웹팩의 주요 속성 소개

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. 웹팩 주요 속성

* entry
* output
* loader
* plugin



## 2. entry

* 웹팩에서 웹 자원을 변환하기 위해 필요한 최초 진입점이자 JavaScript 파일 경로
* entry 속성에 지정된 파일에는 웹 애플리케이션의 전반적인 구조와 내용이 담겨져 있어야 함
* 엔트리 포인트는 1개 또는 여러개
  * 1개인 경우: 싱글 페이지 애플리케이션
  * 2개 이상인 경우: 멀티 페이지 애플리케이션

```JavaScript
// webpack.config.js
module.exports = {
  entry: './src/index.js'
}
```





## 3. output

* 빌드 결과물의 파일 경로
* 최소한 filename을 지정
* 일반적으로 path 속성을 함께 정의

```JavaScript
// webpack.config.js
var path = require('path');

module.exports = {
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, './dist')
  }
}
```



### output 파일 이름 옵션

* 결과 파일 이름에 엔트리 속성을 포함하는 옵션

```JavaScript
module.exports = {
  output: {
    filename: '[name].bundle.js'
  }
};

```



* 결과 파일 이름에 웹팩 내부적으로 사용하는 모듈ID를 포함하는 옵션

```JavaScript
module.exports = {
  output: {
    filename: '[id].bundle.js'
  }
};
```



* 매 빌드시 마다 고유 해시 값을 붙이는 옵션

```JavaScript
module.exports = {
  output: {
    filename: '[name].[hash].bundle.js'
  }
};
```



* 웹팩의 각 모듈 내용을 기준으로 생성된 해시값을 붙이는 옵션

```JavaScript
module.exports = {
  output: {
    filename: '[chunkhash].bundle.js'
  }
};
```





## 4. loader

* 웹팩이 웹 애플리케이션을 해석할 때 웹 자원들을 변환할 수 있도록 도와주는 속성
* 엔트리, 아웃풋과는 달리 module라는 이름 사용

```JavaScript
// webpack.config.js
module.exports = {
  module: {
    rules: []
  }
}
```



# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)

