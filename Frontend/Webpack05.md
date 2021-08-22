# Webpack - 웹팩 개발 서버, API 서버 연동

**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 웹팩 개발 서버

* 인터넷에 웹 사이트를 게시하려면 서버 프로그램으로 이 파일을 읽고 요청한 클라이언트에게 제공해야 함
* 개발환경에서도 이와 유사한 환경을 갖추는 것이 좋다.
  * 배포시 잠재적 문제를 미리 확인할 수 있다.
  * ajax 방식의 api연동은 cors 정책 때문에 반드시 서버가 필요하다.
* **webpack-dev-server** 패키지로 개발용 서버를 사용 가능



## 2. webpack-dev-server

### 기능

* 소스코드를 개발용 서버에서 실행시킬 수 있다.
* 코드 변화를 실시간으로 감지하여 적용한다.

### 설치

* **npm i -D webapck-dev-server**를 입력하여 설치



### 사용법

* package.json에 scripts 등록
  * --progress 옵션을 주면 빌드 상태를 보여줌

```json
{
  "scripts": {
    "start": "webapck-dev-server --progress"
  }
}
```



### 기본 설정

* 웹팩 설정 파일의 devServer 객체에 개발 서버 옵션을 설정할 수 있다.

* contentBase: 정적파일을 제공하는 경로, 기본값은 웹팩 아웃풋

* publicPath: 브라우저를 통해 접근하는 경로. 기본값은 '/'

* host: 개발환경에서 도메인을 맞추는 상황에서 사용

  * 쿠키 기반의 인증은 인증 서버와 동일한 도메인으로 개발환경을 맞춰야 함
  * 운영체제의 호스트 파일에 해당 도메인과 127.0.01 연결을 추가한 뒤 host 속성에 도메인을 설정해서 사용

* overlay: 빌드시 에러, 경고를 브라우저에 표시

* port: 개발 서버 포트 번호를 설정, 기본값은 8080

* stats: 메시지 수준 설정

  * 'none', 'erros-only', 'minimal', 'normal', 'verbose'

* historyApiFallBack: 히스토리 API를 사용하는 SPA 개발시 설정한다. 404 발생시 index.html으로 리다이렉트

  

```JavaScript
// webpack.config.js
module.exports = {
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    publicPath: "/",
    host: "dev.domain.com",
    overlay: true,
    port: 8081,
    stats: "errors-only",
    historyApiFallback: true,
  }
}
```



## 3. API 서버 연동 - 목업 API 만들기 1

* 프론트엔드 개발을 할 때, 목업 API를 만들어 진행하는 것이 수월하다.
  * 목업: 가짜 데이터



### 목업 API 만들기

* webpack.config.js의 devserver 객체에 아래처럼 추가히기

```JavaScript
...
// node의 모듈 시스템
module.exports = {
  ...
  devServer: {
    overlay: true,
    stats: "errors-only",
    // 개발 서버 객체를 받음
    before: (app) => {
      // app: 서버 애플리케이션에서 많이 사용하는 express.js라는 프레임워크의 인스턴스
      // get: get 메소드로 이루어진 api를 만들어내는 함수
      // req: request, res: response
      app.get("/api/users", (req, res) => {
        // res 객체로 api 응답
        res.json([
          {
            id: 1,
            name: "Alice"
          },
          {
            id: 2,
            name: "Bek"
          },
          {
            id: 3,
            name: "Chris"
          }
        ])
      })
    }
  },
  ...
}
```



### axios로 api 호출하기

```JavaScript
import axios from 'axios';

document.addEventListener('DOMContentLoaded', async () => {
  // 페이지가 로딩되었을 때 api요청을 날린다.
  // 요청은 웹팩 개발서버로 날아감
  const res = await axios.get('/api/users');
  // 받은 응답을 html div안에 출력
  document.body.innerHTML = (res.data || []).map(user => {
    return `<div>${user.id}: ${user.name}</div>`
  }).join('');
});
```



## 4. 목업 API 만들기 2

* 목업 API가 많이 필요할 때, 전용 패키지를 사용하는 것이 편하다.
* **connect-api-mocker**: api 응답값을 json으로 만들어 놓고 개발 서버와 연동
  * 응답값을 파일로 관리
  * **npm i -D connect-api-mocker**를 입력하여 설치



### 예시

* **mocks/api/users/GET.json**

```json
[
  {
    "id": 1,
    "name": "Alice"
  },
  {
    "id": 2,
    "name": "Bek"
  },
  {
    "id": 3,
    "name": "Chris"
  },
  {
    "id": 4,
    "name": "Daniel"
  }
]
```



* **webpack.config.js**

```JavaScript
...
const apiMocker = require('connect-api-mocker');
// node의 모듈 시스템
module.exports = {
...
  devServer: {
    overlay: true,
    stats: "errors-only",
    // 개발 서버 객체를 받음
    before: (app) => {
      // express에 미들웨어 추가
      // urlRoot: api로 요청 오는 것은 모커가 처리, pathUrl
      app.use(apiMocker('/api', 'mocks/api'))
    }
  },
 ...
}
```



## 5. 실제 API 연동

* 서버에 직접 api 요청을 하면, CORS 정책으로 인해 응답을 받을 수 없다.
  * CORS: 같은 도메인에서 api 요청을 할 수 있다.
  * 즉, 서버와 도메인이 다르기 때문에 요청이 불가능 하다.



### 서버에서 해결하는 방법

* Access-Control-Allow-Origin헤더를 추가한다.

```JavaScript
// node.js
// server/index.js
app.get('/api/keywords', (req, res) => {
  res.header("Access-Control-Allow-Origin", "*"); // 헤더를 추가
  res.json(keywords)
})
```



### 프론트엔드에서 해결하는 방법

* 웹팩 개발 서버는 porxy 속성으로 해결할 수 있다.

```JavaScript
// webpack.config.js
module.exprots = {
  devServer: {
    proxy: {
      // http://localhost:8081이 서버 일때
      // api라는 url로 요청을 보낼 때 아래 주소로 요청을 보냄
      '/api': 'http://localhost:8081',
    }
  }
}
```

# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)