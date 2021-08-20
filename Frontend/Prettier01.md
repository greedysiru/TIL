# Prettier - 역할, 설치 및 사용법



**본 내용은 인프런 김정환님의 프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..) 강의를 토대로 작성하였습니다.**



## 1. 역할

* 코드를 더 예쁘게 만든다.
* ESLint의 포매팅과 겹치지만 더 일관적인 스타일로 다듬는다.
* 코드 품질 관련 기능은 하지 않음
* ESLint가 고칠 수 없는 코드도 고쳐준다.
  * 긴 문장 자동 수정



## 2. 설치 및 사용법

### 설치

```shell
npm i -D prettier
```



### 사용법

```shell
# CLI에서 prettier의 결과 출력
npx prettier [파일명]
# 파일에 prettier 적용
npx prettier [파일명] --write
```



### ESLint와 통합 방법

* **eslint-config-prettier**: Prettier와 충돌하는 ESLint 규칙을 끄는 역할을 함
  * **npm i -D eslint-config-prettier**을 입력하여 설치
  * **.eslintrc.js**의 extends에 추가하기
* **eslint-plugin-prettier**: Prettier 규칙을 ESLint 규칙으로 추가하는 플러그인
  * **npm -i D eslint-plugin-prettier**을 입력하여 설치
  * **.eslintrc.js**의 plugins와 rules에 설정 추가
* extends에 위의 두 패키지를 함께 사용할 수 있다.
  * **plugin:prettier/recommended**

# Reference

[[인프런]프론트엔드 개발환경의 이해와 실습 (webpack, babel, eslint..)](https://www.inflearn.com/course/프론트엔드-개발환경/dashboard)