# NextJS(2) - Pages, Static Pre Rendering

**본 내용은 Nomad Coders - NextJS 시작하기 강의를 토대로 작성하였습니다.**



## 1. Pages

* NextJS에서 Pages 아래의 파일들을 라우팅 처리 해줌
  * **단, 해당 컴포넌트들은 export default 해야 함**
* index.(js|ts)는 앱의 홈(/)으로 연결 됨
* JSX 사용하여도  React를 import 하거나 확장자를 바꿀 필요 없음
  * useState, useEffect와 같은 hook은 import 해야 함



## 2. Static Pre Rendering

* NextJS는 앱에 있는 페이지들을 미리 렌더링
  * 정적으로 생성 됨



### React.js vs Next.js

* CSR : Client Side Rendering
  * 브라우저가 유저가 보는 모든 UI를 만드는 일을 함
  * React는 기본적으로 CSR
  * id가 root인 div만이 HTML
  * 브라우저가 react.js 그리고 소스 코드를 다운 받아야 UI를 렌더링
  * **브라우저가 JavaScript를 가져와서 모든 UI를 만들게 됨**
  * 네트워크가 느린 유저는 JS 코드를 받아오기전에 흰 화면을 오래 볼 수 있음
  * JavsScript 비활성화 옵션의 경우, 아예 페이지가 뜨지 않음
* Next.js는 페이지들을 미리 렌더링하여 실질적인 HTML 요소를 보여주게 됨
  * 연결 속도가 느리거나 자바스크립트가 비활성화 되어도 볼 수 있음



### Hydration

* React.js를 프론트엔드 안에서 실행하는 것
* 과정
  * Next.js는 React.js를 백엔드에서 동작시켜 페이지를 미리 만듦(Compoent Rendering)
  * HTML을 생성하여 페이지의 소스코드에 넣음(React.js가 로딩되지 않아도 컨텐츠를 볼 수 있음)
  * React.js가 로딩되면, 존재하는 요소들과 연결이 됨
  * 모든 기능이 동작하게 됨
* 단, JavaScript를 비활성화하면 동작하지는 않음



# Reference

[Nomad Coders - NextJS 시작하기](https://nomadcoders.co/nextjs-fundamentals/lobby)

