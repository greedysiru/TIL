# SSR, SSG, JAM Stack

## 1. SSR

* Server Side Rendering
  * 스프링, JSP
* SEO 최적화
* CSR(Client Side Rendering)의 반대
  * React, Vue
  * 자바스크립트를 사용해서 HTML 요소를 동적으로 바꿈
  * 대게 SPA
  * 좋은 UX
  * 규모가 크면 로딩 속도가 길어짐
  * SEO 미흡



## 2. Next.js, Nuxt.js

* Next.js: React의 SSR 페이지 제공 프레임워크
* Nuxt.js: Vue의 SSR 페이지 제공 프레임워크
* 사이트의 원하는 부분을 SSR로 만들 수 있다.
* API 서버로부터 데이터를 서버에서 미리 받아옴(SSR모드)
  * Next.js, Nuxt.js의 서버
  * Node.js가 깔린 서버에서 프로젝트를 어플리케이션으로 실행하여 프론트엔드를 배포
* 바로 나타나야할 것을 정할 수 있음
* SSG(Static Site Generator)
  * 정적 사이트 생성기



## 3. Gatsby

* SSG
* 정보를 json, yaml 등의 정적 파일에 저장
* 이 정보를 React로 렌더링하여 빌드
* 모든 페이지를 컨텐츠가 들어있는 HTML 파일로 생성
* SEO
* 블로그와 같은 방식의 사이트에 사용
* 변하지 않는 페이지를 보여주기 좋다.



## 4. JAM Stack

* JavaScript API Markup Stack
* 웹 서비스 설계 방식
* 정적 사이트 생성기들을 사용한 서비스 설계
* 정적인 프론트엔드 마크업 페이지들을 미리 생성
  * pre-rendering
* 로그인, 결제, 댓글
  * decoupling
* Netlify, Vercel
  * repo를 연결하면, 코드 푸쉬할때마다 빌드까지하여 정적 사이트를 배포
* 정적 페이지를 CDN으로 배포
  * 사용자 경험 개선

# Reference

[SSR, SSG, JAM Stack이 뭔가요? (+ CSR, SEO, Next.js, Nuxt.js, Gatsby)](https://www.youtube.com/watch?v=5ILR9Vd_Vos)

