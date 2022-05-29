# Component와 props

* Component > Element
  * 엘리먼트는 컴포넌트의 구성요소




## 함수 컴포넌트 vs. 클래스 컴포넌트

### 함수 컴포넌트

* 데이터를 가진 props 객체 인자를 받아 React 엘리먼트를 반환
* JavaScript 함수의 형태

```react
function Header(props) {
  return <h1> {props.headerText} </h1>;
}
```



### 클래스 컴포넌트

* ES6 Class를 사용하여 컴포넌트를 정의

```react
class Header extends React.Component {
  render() {
    return <h1> {this.props.headerText} </h1>
  }
}
```



## 컴포넌트 렌더링

* 사용자 정의 컴포넌트를 나타낼 수 있음
* React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견 시, JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달
  * 이 객체를 props라고 함

```react
function Header(props) {
  return <h1>환영합니다. {props.name}님! </h1>
}


const element = <Header name='siru' />
// 엘리먼트로 render 호출
// {name: 'siru'}를 props로 전달
ReactDOM.render(
	element,
  document.getElementById('root');
);
```



## 컴포넌트 합성

* 컴포넌트는 자신의 출력에 다른 컴포넌트를 참조 가능
* React 앱은 최상위에 단일 App 컴포넌트를 가지고 있음

```react
// 페이지를 구성하는 2개의 컴포넌트(Header, Explain)
function Header(props) {
  return <h1>환영합니다. {props.name}님! </h1>
}

function Explain(props) {
  return <span>이 페이지는 {props.name} 입니다.</span>
}

// React의 최상위에 위치할 App 컴포넌트
function App() {
  return (
  	<Header name="siru"></Header>
    <Explain name="React 예시"></Explain>
  )
};

ReactDOM.render(
	<App />,
  document.getElementById('root')
);
```





## 컴포넌트 추출

* 구성 요소들이 중첩 구조로 이루어져 있으면, 변경하기 어려움
* 개별적으로 재사용하기도 어려움
* 컴포넌트를 여러 개의 작은 컴포넌트를 나누기
* UI 일부가 여러 번 사용되거나 UI 일부가 복잡한 경우, 별도의 컴포넌트로 만들 것



## props

* props는 읽기 전용
* 컴포넌트의 자체 props를 수정하면 안 됨
  * **순수 함수**처럼 동작해야 함
  * 순수 함수란, 입력값을 바꾸지 않고 동일한 입력값에대해서 동일한 결과를 반환



# Reference

[React 공식 문서](https://ko.reactjs.org/)