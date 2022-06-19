# 성능 최적화



## 1. 프로덕션 빌드 활용

* React에서 보여주는 경고는 개발에 큰 도움을 주지만, 성능 상 좋지 않음
  * 프로덕션 버전을 사용해야 함
* React Developer Tools for Chrome Extenstion을 사용하여, 프로덕션 빌드가 되어있는지 확인 가능



## 2. Create React App

* 아래 명령어를 실행하면, build 디렉토리 아래에 애플리케이션 프로독션 빌드파일이 만들어 짐

```shell
npm run build
```



## 3. webpack

* webpack v4 이상에서는 프로덕션 모드에서 기본적으로 코드를 축소

```JavaScript
const TerserPlugin = require('terser-webpack-plugin');

module.exports = {
  mode: 'production',
  optimization: {
    minimizer: [new TerserPlugin({ /* 옵션 */ })]
  },
};
```

# Reference

[React 공식 문서](https://ko.reactjs.org/)

