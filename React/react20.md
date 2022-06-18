# JSX 이해하기

* React.createElement() 함수에 대한 문법적 설탕

```React
React.createElement(
	Header,
  {color: 'teal'},
  '헤더입니다.'
)

--------------------------------------
// 아래의 코드는 위와 같이 컴파일 됨
<Header color='teal'>
  	헤더입니다.
</Header>
```



## 1. React Element 타입 지정

* JSX 첫 부분은 React Element의 타입을 결정
* 대문자로 시작

```React
<Header />
```



## 2. React가 스코프 내에 존재해야 함

* 위 대로, JSX는 React.createElement의 문법적 설탕
  * 그러므로, 같은 스코프 내에 React를 import
* script 태크를 통해 React를 불러온 경우, React는 전역변수이므로 import할 필요 없음

```React
import React from 'react';

function Header = () => {
  return <h1>헤더입니다.</h1>
}
```



## 3. JSX 점 표기법

* 점 표기법을 사용하여 React 컴포넌트 참조 가능

```React
import React from 'react';

const Text = {
  title: () => {
    return <h1>헤더입니다.</h1>
  }
}

const Header = () => {
  return <Text.title />
}
```



## 4. JSX 안에서의 prop 사용

* JavaScript 표현식을 중괄호 안에 넣어서 JSX 안에서 prop으로 사용 할 수 있음
* 문자열 리터럴은 prop으로 넘길 수 있음
* props의 기본값은 true
* porps에 해당하는 객체를 스프레드 연산자로 사용해 전체 객체로 넘길 수 있음

```React
const Header = props => {
  const {className, ...other} = props;
  return <h1 className={className} {...other}></h1>
}
```



## 5. JSX에서 자식 다루기

* 여는 태그와 닫는 태그가 있는 JSX에서 사이에 있는 내용은 props.children으로 넘겨짐
* props.children
  * 문자열 리터럴
  * JSX
  * JavaScript 표현식
  * 함수
  * boolean, null, undefined는 무시 됨
  * 0과 같은 falsy 값들은 React가 렌더링 함에 주의

# Reference

[React 공식 문서](https://ko.reactjs.org/)

