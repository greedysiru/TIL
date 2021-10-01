# 실전으로 배우는 타입스크립트 - 프로젝트 환경 구성

**본 내용은 인프런 장기효(캡틴판교)님의 실전으로 배우는 타입스크립트 강의를 토대로 작성하였습니다.**



## 1. 타입스크립트 개발 환경 관련 라이브러리 설치

* 타입스크립트 및 문법 검사, 코드 정리 도구 라이브러리 설치
  * devDEpendencies로 설치

```shell
npm i -D typescript @babel/core @babel/preset-env @babel/preset-typescript @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint prettier eslint-plugin-prettier
```



## 2. ESLint

### ESLint 소개

* JavaScript 코드에서 문제를 찾아 고침
* 런타임 에러를 코드레벨에서 미연에 방지
* 코드 문법 보조 도구
* 코드 자동완성, 포매팅을 지원
* ESLint를 사용하는 이유?
  * TSLint보다 ESLint가 성능상 더 좋음



### Rules

* ESLint가 어떤 규칙을 가지고 코드를 검증해나갈 지를 정의한 속성
* 맞지 않는 것들에 대해서 에러를 알려줌



### .eslintrc.js

* "off" or 0 : 규칙을 끔
* "warn" or 1: 규칙을 키고 위반시 경고
* "error" or 2: 규칙을 키고 위반시 에러
* js, json, yml 확장자 사용 가능

```JavaScript
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true,
  },
  extends: [
    // eslint 권장 기본 옵션
    'eslint:recommended',
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  // 플러그인
  // eslint-plugin-prettier를 설치하여 prettier를 eslint에서 인식
  plugins: ['prettier', '@typescript-eslint'],
  rules: {
    'prettier/prettier': [
      'error',
      {
        singleQuote: true,
        semi: true,
        useTabs: false,
        tabWidth: 2,
        printWidth: 80,
        bracketSpacing: true,
        arrowParens: 'avoid',
      },
    ],
  },
  parserOptions: {
    parser: '@typescript-eslint/parser',
  },
};
```



### 플러그인 옵션 설정

* VSCode의 ESLint 플러그인 설치
* **cmd + shift + p** 키를 이용하여 명령어 실행 창 표시
* 명령어 실행 창에 **open settings (json)** 입력 후 선택
* setting.json 파일에서 설정 추가
  * VSCode 사용자 설정 파일
* preference에서 format on save가 꺼져있어야 함
  * 포매터와 ESLint와 충돌이 나는 것을 방지

```json
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true
},
"eslint.alwaysShowStatus": true,
"eslint.workingDirectories": [
  {
    "mode": "auto"
  }
],
"eslint.validate": [
  "javascript",
  "typescript"
],
```



### setting.json

```json
{
    ...
 	 // 저장을 하면 eslint가 코드에서 에러가 나는 부분을 수정
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
  	// 각 디렉토리별 elsint를 구분하도록 하는 설정
    "eslint.workingDirectories": [
          {
              "mode": "auto"
          }
      ],
    ...
}
```



### .eslintignore

* ESLint를 적용하지 않을 파일이나 디렉토리 지정



## 3. 바벨

### 바벨 소개

* 자바스크립트 컴파일러
  * 정확히는 트랜스파일러
* 최신 자바스크립트 문법이 여러 브라우저에서 호환되도록 도와줌



### preset

* 플러그인과 옵션의 집합
* **@babel/core**
  * 바벨과 관련된 기본 코어
* **@babel/preset-typescript**
  * 타입스크립트와 함께 사용할 때 설치



## 4. Prettier

### Prettier 소개

* 취향대로 설정할 수 있는 코드 포매터
  * 코딩 컨벤션에 맞출 수 있음



### Prettier 옵션

* 한줄의 길이 설정
* 탭 간격
* 세미콜론 여부
* 그외 등등



### Prettier 옵션 .eslintrc.js에 정의하기

```JavaScript
module.exports = {
  ...
  rules: {
    'prettier/prettier': [
      // prettier에 위배되면 에러 발생
      'error',
      {
        singleQuote: true,
        semi: true,
        useTabs: false,
        tabWidth: 2,
        printWidth: 80,
        bracketSpacing: true,
        arrowParens: 'avoid',
      },
    ],
  },
  ...
};
```



# Reference

[실전 프로젝트로 배우는 타입스크립트](https://www.inflearn.com/course/타입스크립트-실전/dashboard)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)