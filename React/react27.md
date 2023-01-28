# React 완벽 가이드 - 시작하기



**본 내용은 Udemy의 React 완벽 가이드 with Redux, Next.js, TypeScript 강의를 토대로 작성하였습니다.**



## react.js란

* A Client-side JavaScript Library
* 웹사이트를 위한 반응형 UI interface를 만드는 데 사용
* 애플리케이션에 가까운 사용자 경험 제공
  * 원활한 화면 전환
* JavaScript는 프로그래밍 언어로 브라우저에서 로직을 실행할 수 있음
  * DOM을 조작할 수 있음
  * 이를통해 새로운 HTML 페이지를 불러오지 않고 사용자들이 보는 것을 변경할 수 있음



### vs. 전통적인 웹사이트

* 브라우저가 필요한 페이지를 서버에 요청 -> 서버는 새로운 HTML 페이지를 브라우저로 응답
  * HTML이 로딩되는 동안 기다려야만 했음



## JavaScript대신 react.js를 쓰는 이유

* JavaScript로 App을 구현하기 위해서는 모든 단계를 일일히 작성해야 함
  * 명령형 프로그래밍
  * 요소를 생성하고 텍스트 컨텐츠를 설정하는 것과 같은 되풀이되는 반복적인 로직을 작성해야 함
* react.js는 사용자 지정 HTML 컴포넌트를 사용할 수 있음
  * JSX 문법: JavaScript 확장 문법
  * app을 작은 컴포넌트들로 분할할 수 있음
  * 코드를 유지보수 관리가 용이하게 할 수 있음
  * 요소를 생성하고 텍스트 컨텐츠 설정하는 일은 react.js에게 위임
  * 선언형 프로그래밍
  * 화면에 나타내고 싶은 것, 최종 목표로 하는 것에 집중할 수 있음



## React로 SPA 구축하기

* SPA: Single Page Application
  * React는 주로 SPA를 구축하는데에 사용
  * 화면을 전환할 떄 서버로부터 새로운 HTML을 요청하지 않음
  * 전환할 때 JavaScript가 기능하는 것
* MPA: Multi Page Application
  * React는 종종 MPA에서 일부분으로써 사용될 수 있음



### React의 대안들

* React는 컴포넌트 기반 UI 라이브러리
* 컴포넌트에 중점을 둠
* 내장된 다른 기능은 많지 않음
  * ex) 라우팅이 필요하면 추가적인 라이브러리 설치가 필요
* 가장 점유율이 큼



### vs. Angular

* 컴포넌트 기반의 UI 라이브러리
  * React와는 다른 방식을 컴포넌트를 구축하고 문법또한 다른점이 있음
* 점유율이 크지는 않음
* 내장된 많은 기능이 있음
  * 소규모의 프로젝트에는 과할 수 있음
  * 대규모의 프로젝트에서는 유용
  * 커뮤니티 의존성 낮음
* 처음부터 TypeScript를 수용



### vs. Vue.js

* Angular + React.js를 합친 형태
* 컴포넌트 기반의 UI 프레임워크
* 내장된 기능이 있음
  * Angular보다는 적고, React.js보다는 많음
  * Routing같은 핵심 기능 포함




## Reference

[[Udemy] React 완벽 가이드 with Redux, Next.js, TypeScript](https://www.udemy.com/course/best-react/)

