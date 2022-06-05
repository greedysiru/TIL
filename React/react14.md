# 합성 vs 상속

* 합성을 사용하여 컴포넌트간의 코드를 재사용하는 것이 좋음



## 컴포넌트에서 다른 컴포넌트를 담기

* 어떤 자식 엘리먼트가 들어올 지 미리 알 수 없는 경우 children prop을 사용하여 자식 엘리먼트를 그대로 전달
* children 대신 다른 프로퍼티로 JSX를 전달할 수 있음
* React 엘리먼트는 객체이므로 prop으로 전달 가능

```React
function Header(props) {
  return (
  	<div>
    	{props.children}
    </div>
	);
}

-------------------------------------------------------------------------

function mainPage(props) {
  return (
  	<Header>
      <!-- JSX태그 안에 있는 것들이 children prop으로 전달 됨 -->
    	<h1>헤더입니다.</h1>
    </Header>
  )
}
```



## 특수화

* 정의한 컴포넌트를 토대로 특수한 경우에 사용할 컴포넌트를 정의

```React
function Header(props) {
  return (
    <div className="Header">
      <h1 className="Header-title">
  	    {props.title}
	    </h1>
      <p className="Header-content">
      	{props.content}
      </p>
    </div>
  )
}

-------------------------------------------------------------------------

function SignupHeader() {
  const [nickName, setNickName] = useState();
  const handleChange = (e) => {
    setNickName(e.target.value);
  }
  const handleSignUp = () => {
    console.log(`${nickName}으로 회원가입을 요청합니다.`);
  }
  
  return (
  	<Header 
      title="회원가입"
      contents="정보를 입력하세요"
    >
      <input value={nickname} onChange={handleChange}></input>
      <button onClick={handleSignUp}>회원가입</button>
    </Header>
  )
}
```







# Reference

[React 공식 문서](https://ko.reactjs.org/)

