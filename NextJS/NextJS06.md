# NextJS(6) - next config(Redirect, Rewrite)

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. next.config.js

* NextJS 프로젝트의 설정 파일
* Node.js 모듈
* Redirect, Rewirte 등을 정의할 수 있음



## 2. Redirect

* 특정 url에 대한 접근을 지정한 url로 이동처리 할 수 있음
* params도 인식할 수 있음
* Properties
  * source: 특정 url
  * detination: 지정할 url
  * permanent: cache 설정(boolean)



### 예시

```JavaScript
module.exports = {
  reactStrictMode: true,
  async redirects() {
    return [
      {
        source: "/example",
        destination: "/home",
        permanent: false,
      },
    ];
  },
};

```



## 3. Rewrite

* 특정 경로를 다른 경로로 mapping
* URL 프록시 역할을 함
* destination 경로를 masking
* 사용자에게 api 정보를 가릴 수 있음
  * 환경 변수와 활용하면 사용자에게 api 호출에 관련된 정보를 가릴 수 있음
* Properties
  * source: 요청 받는 특정 경로
  * destination: 요청을 돌릴 다른 경로(mapping할 경로)



### 예시

```JavaScript
const API_KEY = process.env.API_KEY;

module.exports = {
  reactStrictMode: true,
  async rewrites() {
    return [
      {
        source: "/api/user",
        destination: `https://api.myapi.co/user?api_key=${API_KEY}`,
      },
    ];
  },
};

```




# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

