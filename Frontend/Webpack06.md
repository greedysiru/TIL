# Webpack - 핫로딩

**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 핫 모듈 리플레이스먼트(HMR)

* 변경된 모듈만 새로고침 하는 것
  * 나머지 모듈은 유지됨
* 화면 개발시 효율적으로 빠르게 할 수 있다.



### 설정

* **webpack.config.js**의 **devServer** 객체에 **hot** 추가

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
      // express에 미들웨어 추가
      // urlRoot: api로 요청 오는 것은 모커가 처리, pathUrl
      app.use(apiMocker("/api", "mocks/api"))
    },
    hot: true
  },
  ...
}
```



## 2. HMR의 사용법

* 설정 이후, 제공하는 모듈을 HMR 인터페이스에 맞추어야 한다.

```JavaScript
// app.js
import result from "./result";

let resultEl

document.addEventListener("DOMContentLoaded", async () => {
  resultEl = document.createElement("div");
  resultEl.innerHTML = await result.render();
  document.body.appendChild(resultEl);
})

// HMR을 켜면, 모듈 객체의 hot에 들어오게 됨
if (module.hot {
    console.log("핫 모듈 켜짐");
		// accpet함수이 인자로 변경을 감지할 모듈 입력
		// 해당 모듈의 변화가 감지되면 콜백함수 실행
		module.hot.accept("./result", async () => {
      console.log("result 모듈 변경됨");
      // 업데이트 된 result 모듈의 render 함수의 결과를 넣음
      resultEl.innerHTML = await result.render();
    });
}
```



## 3. 핫 로딩을 지원하는 로더

* HMR을 사용하기 위해서는 위처럼 모듈이 HMR 인터페이스를 구현해야 한다.
* style-loader, file-loader, react-hot-loader

# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)

