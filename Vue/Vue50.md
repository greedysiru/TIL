

# Vue.js - Netlify, env

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1. Netlify

* 호스팅 서비스
* Github repository를 연동하여 배포할 수 있음
  * 브랜치도 선택 가능
* 배포를 진행하며 실행된 로그를 볼 수 있음



### SPA 호스팅 시에 추가할 것

* Netlify에서 SPA를 배포했을 때 페이지에 Not found가 뜨며 접근이 안될 수도 있음
* 서버에 추가해야하는 설정 필요
* SPA는 특정 페이지의 정보를 브러우저에서 가지고 있으므로 서버에서 접근이 불가능
* 모든 url 접근을 index.html에 돌리는 redirect 설정을 해야 함
  * [참고](https://cli.vuejs.org/guide/deployment.html#netlify)



## 2. env 환경 변수

* env 파일
  * 배포시에 필요한 옵션을 담는 파일
* 변수=값의 형식
* Application Layer에서 접근 불가
  * 접근하기 위해서는 웹팩 define plugin 필요(Vue 2 버전)
  * VUE_ prefix 를 붙이면 Application에서 접근 가능
* process.env로 접근

```
// .env
CAT_NAME=SIRU
VUE_CAT_NAME=SIRU
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

