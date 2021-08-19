# ESLint



**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 등장 배경

* lint: 보푸라기
* 코드의 작은 보푸라기를 제거하는 것
  * 가독성을 높이는 것
* 예상하지 못한 런타임 버그를 예방
* 검사하는 항목
  * 포맷팅: 코드의 일관성(들여쓰기, 줄길이)
  * 코드품질: 코드의 오류 유발 가능성 줄이기



## 2. 설치 및 사용법

### 설치

```shell
npm i -D eslint
```



### 사용법

* **.eslintrc.js**: ESLint의 설정 파일
* **Rules**를 입력하여 규칙 설정
* **npx eslint 파일명**을 입력하여 규칙에 위배되는지 체크
  * **--fix**:규칙에 어긋나는 것을 바로 수정하는 옵션
  * **--init**: 어떻게 사용할 것인지를 CLI로 체크하여 **.eslintrc.js 설정**

```JavaScript
// .eslintrc.js
module.exports = {
  rules: {
    // 규칙에 어긋나면 오류 반환
    "no-unexpected-multiline": "error",
    "no-extra-semi": "error"
  }
}
```



## 3. Extensible Config

* 규칙을 여러개 미리 정해 놓은 것
  * **eslint:recomended**: ESLint에서 추천하는 설정
  * aribnb, standard 등이 있음

```JavaScript
module.exports = {
  extends: [
    "eslint:recommended"
  ]
}
```



# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)