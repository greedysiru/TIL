# Node.js와 NPM

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. Node.js

* JavaScript 실행 환경



## 2. NPM

* Node Package Manager
* JavaScript 프로그래밍 언어를 위한 패키지 관리자



### NPM 시작하기

* 버전 확인

```shell
node - v
npm - v
```



* 프로젝트 생성
  * 프로젝트에 대한 여러 설정을 입력
  * package.json 생성
  * -y 옵션 입력시, 설정 입력을 생략 가능

```shell
npm init -y
```



* 패키지 설치
  * node_modules 아래에 설치 됨
  * packages.json의 dependencies에 설치한 패키지가 기록

```shell
npm install [라이브러리 명]
```



## 3. NPM의 장점

* 라이브러리 관리하기 용이
  * package.json에 정리되어 있으므로
  * 사용된 라이브러리
  * 라이브러리 버전
* 라이브러리를 검색하기 용이
* 컴퓨터 환경에 라이브러리가 설치
  * 라이브러리 접근이 편함



# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)

