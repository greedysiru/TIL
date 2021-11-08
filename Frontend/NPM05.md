# NPM 명령어

**본 내용은 인프런 장기효(캡틴판교)님의 프론트엔드 개발자를 위한 웹팩 강의를 토대로 작성하였습니다.**



## 1. NPM 지역 설치 & 제거

### 지역 설치

```shell
npm install [패키지명]
# 위와 같음
npm i [패키지명]
```

* --save-prod 옵션이 생략되어도 지역 설치
* 해당 패키지가 **node_modules**에 설치
  * 패키지와 관련된 패키지도 설치
* package.json의 dependencies에 해당 패키지와 버전이 기록



### 지역 제거

```shell
npm uninstall [패키지명]
```

* node_modules와 package.json의 dependencies에서 삭제됨



### 지역 설치 명령어 옵션

```shell
npm install [패키지명] --save-prod

npm install [패키지명] --save-dev
# 위와 같음
npm install [패키지명] -D
```

* **--save-prod**
  * dependencies에 설치
* **--save-dev**
  * devDependencies에 설치



## 2. NPM 전역 설치

### 전역 설치

```shell
npm install [패키지명] --global
```

* node_modules가 아닌, 시스템 전역에 설치 됨
* 시스템 상에서 해당 패키지를 제어할 수 있는 명령어가 있음



### 전역설치된 라이브러리 경로

```shell
# window
%USERPROFILE%\AppData\Roaming\npm\node_modules

# mac
/usr/local/lib/node_modules
```



## 3. dependencies vs. devDependencies

* dependencies: 애플리케이션 로직과 연관
  
  * 배포용 라이브러리
  * react, vue 등
  
* devDependencies: 개발할 때 도움을 주는 보조 패키지

  * 개발용 라이브러리

  

### 배포용 라이브러리와 개발용 라이브러리 구분하기

* 배포용 라이브러리(dependencies)는 **npm run build**로 빌드 시에 최종 애플리케이션 코드 안에 포함
* dependencies에 필요없는 패키지가 들어가면, 빌드 시간이 오래 걸림

# Reference

[[인프런]프론트엔드 개발자를 위한 웹팩](https://www.inflearn.com/course/%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9/dashboard)

