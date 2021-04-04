# JSX

* JavaScript를 확장한 문법
* React element를 생성
* 문자열도 HTML도 아니다.
  * 태그 문법을 사용하나 다른 점들이 있다.



## 1. JSX에 표현식 포함하기

```React
const name = 'greedy siru';
const element = <h1>Hello, {name}</h1>
      
ReactDOM.render(
	element,
  document.getElementById('root')
)
```

* 중괄호 안에 JavaScript 표현식을 넣을 수 있다.
* 수식, 함수 등 사용할 수 있다.



## 2. JSX는 표현식이다

* 컴파일이 끝나면 JSX 표현식이 정규 JavaScript 함수 호출이되고 JavaScript 객체로 인식된다.
* if, for에 사용할 수 있다.
* 변수에 할당, 인자, 함수로부터 반환이 가능하다.



## 3. JSX 속성 정의

```React
const element = <img src={user.avatarUrl}></img>;
const element = <div className="hi"></div>;
```

* 중괄호를 사용하여 속성에 JavaScript 표현식 삽입
* 속성에 따옴표를 사용하여 문자열 리터럴을 정의할 수도 있다.
* 여기서 속성은 소문자로 시작하는 camelCase 규칙을 사용한다.

# Reference

[React 공식 문서](https://ko.reactjs.org/)