# Webpack - 로더



**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 로더의 역할

* Webpack은 모든 파일을 모듈로 취급한다.
  * JavaScript 뿐만 아니라, 스타일 시트, 이미지, 폰트까지 모두 모듈로 봄
  * import(ES6) 구문을 사용하면 JavaScript 코드 안으로 가져올 수 있다.
* 로더가 모든파일을 JavaScript의 모듈처럼 만들어준다.
  * 이미지 파일 -> data URL 형식의 문자열
  * CSS -> JavaScript에서 직접 로딩할 수 있도록 함



## 2. 커스텀 로더 만들기

### 로더 파일 정의

```JavaScript
// my-webpack-loader.js
module.exports = function myWebpackLoader(content) {
  // 처리할 파일을 만나면 console.log 명령어를 alrert로 변환한다.
  return content.replace('console.log(', 'alert(');
}
```



### webpack.config.js

```JavaScript
...
module.exports = {
...
  module: {
    rules: [
      {
        // 로더가 처리해야할 파일의 패턴(정규표현식)
        // .js로 끝나는 모든 파일
        test: /\.js$/,
        // 사용할 로더를 명시(절대 경로)
        use: [
          path.resolve('./my-webpack-loader.js')
        ]
      }
    ]
  }
}
```

* 로더는 module 객체의 rules라는 배열에 객체의 형태로 추가할 수 있다.
  * test는 로더가 처리할 파일의 패턴(정규 표현식)
  * use는 path.reslove로 로더의 절대경로를 입력
* 빌드를 하게 되면, 웹팩은 엔트리포인트부터 시작해서 연결된 모든 모듈을 검색한다. .js로 끝나는 파일들을 만나면 로더가 실행되어 console.log 명령어를 alret로 바꾸게 된다.



## 3. 자주 사용하는 로더

### css-loader

* JavaScript에서 CSS파일을 모듈로 불러올 수 있다.
* ES6 문법인 import로 CSS파일을 불러오기 위해서는 CSS파일이 모듈이 되어야 한다. 로더가 이를 처리해준다.
* **npm i css-loader**를 입력하여 로더 설치
* **webpack.config.js**에 아래와 같이 입력

```JavaScript
...
module.exports = {
 ...
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'css-loader'
        ]
      }
    ]
  }
}
```



### style-loader

* CSS-loader만 사용해서는 스타일이 적용되지 않는다.
  * CSS코드는 CSSOM으로 바뀌어야 브라우저에서 표현된다.
  * HTML에서 CSS 코드를 불러오거나
  * inline으로 스타일을 넣는다.
* JavaScript로 처리된 스타일 코드(문자열)를 HTML에 넣어주는 로더
* **npm i style-loader**를 입력하여 로더 설치
* **webpack.config.js**에 로더 추가
  * 순서는 뒤에서부터 앞으로

```JavaScript
...
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      }
    ]
  }
}
```



### file-loader

* 이미지 파일을 모듈로 변환하여 import할 수 있게한다.
* 빌드시, 이미지 파일 명을 해시값으로 바꾼다.
  * 웹팩은 빌드할 때마다 유니크한 값을 생성
  * 정적 파일의 경우(JavaScript, CSS, 이미지, 폰트) 브라우저에서 캐시를 하는데 캐시 갱신을 위함
  * 파일이 달라져도 이름이 같으면 브라우저가 이전의 파일을 사용하기 때문
* **npm i file-loader**를 입력하여 로더 설치
* **webpack.config.js**에 로더 추가

```JavaScript
...
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      },
      {
        test: /\.png$/,
        loader: 'file-loader',
        options: {
          // 파일로더가 처리하는 파일을 모듈로 사용했을 때 경로 앞에 추가되는 문자열
          publicPath: './dist',
          // 파일로더가 output에 복사할 때 사용하는 파일명
          // 쿼리스트링 뒤에 hash를 사용하여 캐시 무력화
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  }
}
```



### url-loader

* 사용하는 이미지 갯수가 많아지면 네트워크 부담이 된다.
  * 사이트 성능에 영향
* 한 페이지에서 작은 이미지 여러개를 사용할 때 **Data URI Scheme**를 사용하는 방법이 낫다.
  * img태그의 src에 data 포맷, 인코딩방식, 그 값을 적어준다.
  * 주소를 넣으면 한번 더 네트워크 통신을 하지만 값을 적어주면 네트워크 통신을 하지 않으므로 더 효율적
* **npm i url-loader** 입력하여 로더 설치
* **webpack.config.js**에 로더 추가

```JavaScript
...
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'url-loader',
        options: {
          // 파일로더가 처리하는 파일을 모듈로 사용했을 때 경로 앞에 추가되는 문자열
          publicPath: './dist',
          // 파일로더가 output에 복사할 때 사용하는 파일명
          name: '[name].[ext]?[hash]',
          // 20kb 미만인 파일들은 url-loader가 처리, 이상인 경우 file-loader가 처리
          // base-64로 변환
          limit: 20000,
        }
      }
    ]
  }
}
```


# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)