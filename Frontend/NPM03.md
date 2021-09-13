# NPM

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. Npm 명령어

### 라이브러리 지역 설치

```shell
npm install [라이브러리명]
```

* node_modules 디렉토리 아래에 설치
* 라이브러리와 관련된 라이브러리(의존적인)를 자동 설치
* --save-prod 옵션과 같음(기본값)



### 라이브러리 삭제

```shell
npm uninstall [라이브러리명]
```

* 라이브러리와 해당 라이브러리와 관련된 의존적인 라이브러리들을 삭제



### 라이브러리 전역 설치

```shell
npm install [라이브러리명] --global
```

* 라이브러리를 전역 설치
* node_modules가 아닌 시스템에 설치가 된다.
  * mac 기준 경로: /usr/local/lib/node_modules
  * window 기준 경로: %USERPROFILE%\AppData\Roaming\npm\node_modules
* 시스템에 설치하여 라이브러리가 제공하는 CLI 명령어 기능을 사용할 수 있다.



### 지역 설치 옵션

```shell
npm install [라이브러리명] --svae-prod
-> 축약형 npm install [라이브러리명]

npm install [라이브러리명] --save-dev
-> 축약형 npm install [라이브러리명] -D
```

* --save-dev
  * devDependencies에 라이브러리가 등록



## 2. dependencies vs. devDependencies

* dependencies: 배포용 라이브러리
  * 애플리케이션 로직과 연관이 있는 경우
  * 빌드 시(npm run build) 최종 애플리케이션 코드 안에 포함됨
  * react, angular...
* devDependencies: 개발용 라이브러리
  * 개발을 도와주는 보조 라이브러리의 경우
  * 빌드 시(npm run build) 최종 애플리케이션 코드 안에 포함되지 않음
  * webpack, sass
* 잘 구분하여야 빌드의 시간을 단축시킬 수 있다.

# Reference

[프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/프런트엔드-웹팩)