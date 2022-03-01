

# Vue.js - ESLint 규칙, 파일 경로

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 끝장내기 - 실무에 필요한 모든 것 강의를 토대로 작성하였습니다.**

## 1. ESLint 규칙

### 프로젝트 레벨로 ESLint 규칙을 관리해야하는 이유

* 프로젝트의 코드 레벨에서 ESlint 규칙 설정이 되어있으므로 GitHub를 통해 코드를 받아 작업하는 협업자들이 동일한 설정에서 작업이 가능
* 개발툴의 종류에 영향을 받지않고 작업 가능



## 2. 파일 경로

* 상대 경로를 사용하면, 파일의 레벨이 깊어질 수록 경로가 복잡해짐
  * import를 하여 컴포넌트나 모듈을 불러올 시, 복잡해짐
* 특정 위치를 기준으로 절대 경로로 찾기 설정할 것



### 절대 경로 설정

* jsconfig.json: VSC 내부 기능 활용을 위한 설정 파일

```Json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "~/*": [
        "./*"
      ],
      // 절대 경로 설정
      "@/*": [
        "./src/*"
      ],
    }
  },
  // complierOptions에 해당하지 않을 것들
  "exclude": [
    "node_modules",
    "dist"
  ]
}
```





# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js-%EB%81%9D%EB%82%B4%EA%B8%B0-%EC%BA%A1%ED%8B%B4%ED%8C%90%EA%B5%90/dashboard)