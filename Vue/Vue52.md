

# Vue.js - Vue 설정, Webpack Dev Server

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**



## 1. Vue 설정

### vue.conifg.js

* Vue의 설정을 정의할 수 있는 파일

```JavaScript
module.exports = {
  devServer: {
    // ESLint 오류가 화면을 덮지 않도록 설정
    overlay: false,
  },
};

```



## 2. Webpack Dev Server

* 웹 애플리케이션 개발에 유용한 도구
* 코드가 변경되면 웹팩으로 빌드 후 브라우저를 새로고침
* 빌드 결과물이 프로젝트 폴더에서 보이지 않음
  * 결과물이 메모리에 저장
  * 컴퓨터 관점에서, 메모리 입출력이 컴퓨터 자원이 덜 소모 됨
* 프록시 기능을 사용하여, 로컬 환경 개발시 CORS 문제 해결할 수 있음
* 설정 파일들을 바꾼 경우에는 Dev Server를 재시작해야함



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)