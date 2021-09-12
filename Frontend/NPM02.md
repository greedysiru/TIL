# Node.js와 NPM

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. Node.js와 NPM 소개

### Node.js

* 브라우저 밖에서도 JavaScript를 실행할 수 있는 환경



### NPM

* Node Package Manager
* JavaScript 프로그래밍 언어를 위한 패키지 관리자
  * 라이브러리 관리 도구
  * 모든 라이브러리를 관리하고 있음



## 2. NPM 시작하기

### package.json 초기화

```shell
npm init
```

* 패키지 이름, 버전 등을 입력하여 package.json 생성
* -y: 기본값으로 package.json을 바로 생성하는 옵션



### 패키지 설치

```shell
npm install [패키지명]
```

* node_modules 디렉토리 아래에 패키지가 설치(지역 설치)
  * --save-prod옵션과 같은 효과
* package.json에 패키지와 버전이 기록됨
  * dependencies에 정리
* --global: 시스템 레벨에서 사용할 라이브러리를 설치할 때 사용하는 옵션
  * -g로 축약 가능



## 3. NPM 장점

### 이전 웹개발 방식

* 필요한 라이브러리를 script태그로 가져옴
* 문제점
  * 라이브러리 버전을 관리하기 어려움
  * 라이브러리 간의 의존 관계를 관리하기 어려움
  * 필요한 패키지를 하나하나 검색하여야 함(cdn)
  * 개발 규모가 커질 수록 위의 어려움이 기하급수적으로 증가
* NPM의 경우 
  * package.json에서 패키지들을 관리하기 용이
  * npm install 명령어로 패키지를 설치

# Reference

[프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/프런트엔드-웹팩)