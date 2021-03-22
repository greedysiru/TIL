# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (2) (2021.3.20)



# 1. React 프로젝트 만들기

## 1.1 NVM

* **Node Version Manager**
* Node.js의 버전 관리자
* node를 설치하는 툴

### CLI 명령어

```shell
# nvm 버전 확인
nvm --version
# node.js 설치
nvm install [설치할 버전]
# nvm 으로 설치한 노드 버전 리스트 확인
nvm ls
# 노드 버전 확인 명령어
node -v 
# 노드 버전 바꾸기
nvm use [사용할 노드 버전]
```



## 1.2 npm, yarn

* NPM(Node Package Manager : third-party 패키지를 활용할 수 있다.
* yarn 또한 패키지 매니저
* 프론트엔드 의존성을 관리하기 위한 패키지 매니저들
* 패키지 : 누가 만들어 놓은 코드



### npm으로 yarn 설치하기

```shell
# 옵션은 필요한 경우에 적기
# npm install [옵션] [설치할 패키지 이름]
npm install -g yarn
# -g 옵션: 컴퓨터 전체 설치
```



### yarn으로 패키지 설치

```shell
yarn add [옵션] [설치할 패키지 이름]
```



### CRA(crate-react-app)

* 웹사이트를 만들 때 필요한 것을 모두 넣은 패키지
* yarn으로 설치

```shell
yarn add global create-react-app
```

* 설치 후 프로젝트 만들기

```shell
yarn create react-app [프로젝트 이름]
```

* 리액트 앱 실행

```shell
cd [프로젝트 디렉토리]
yarn start
```



# 2. JSX

* JavaScript를 확장한 문법
* React와 함께 사용

## JSX 규칙

### 태그는 닫기

* input 태그같은 경우도 닫아주어야 한다.

```react
<input type='text'/>
```



### 무조건 1개의 엘리먼트를 반환

* return 안에는 한 개의 엘리먼트로 묶어서 반환하도록 한다.

```react
// 맞는 경우
return (
<p>리액트</p>
)
// 틀린 경우
return (
<div>리액트</div>
<p>리액트</p>
)
```



### JSX에서 JavaScript 값을 가져올 때

* 중괄호를 사용

```react
const cat_name = 'siru';
return (
<div>
  my cat is {cat_name}
</div>
)
```

* 값을 가져올 때 뿐만 아니라, map,  삼항 연산자 등 자바스크립트 문법을 JSX 안에 쓸 때도 {}를 이용

```react
return (
    <div className="App">
      <p>리액트 입니다.</p?
      <p>{number > 10 ? number+'은 10보다 크다': number+'은 10보다 작다'}</p>
    </div>
  );
```



### class 대신 className

```react
<div className = "App"></div>
```



### 인라인으로 style 주기

* json 형식으로 넣어준다.
* 딕셔너리를 중괄호 두 번 사용하는 이유
  * 딕셔너리도 자바스크립트 이므로

```react
<p style={{color: 'orange', fontSize: '20px'}}>orange</p>

//혹은 스타일 딕셔너리를 변수로 만들고 사용
function App() {
  const styles = {
    color: 'orange',
    fontSize: '20px'
  };

  return (
    <div className="App">
      <p style={styles}>orange</p>
    </div>
  );
}
```





# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)

