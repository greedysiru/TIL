# 조건부 렌더링

* JavaScript에서의 조건 처리와 같이 동작
  * if나 삼항 연산자를 활용하여 상태에 맞는 엘리먼트를 조건부 렌더링
* 조건이 복잡하다면, 컴포넌트를 분리할 때
* 상황에 따라, 가독성이 좋은 방법을 사용하기
* 특정 상황에서 컴포넌트 렌더링을 막으려면, 조건부로 null을 return하면 됨



## 예시(if)

* 로그인 상태에 따라 Header 컴포넌트의 문구를 다르게 출력

```React
function Header(props) {
  // 부모로부터 유저가 로그인하였는지에 대한 값을 받음(boolean)
  const {isLoggedIn} = props;
  
  // 로그인을 한 상태면, 인사를
  if (isLoggedIn) {
    return <h1>안녕하세요! 환영합니다.</h1>;
  } else {
    // 로그아웃을 한 상태면, 로그인을 할 것을 보여줌
    return <h1>로그인을 해주세요.</h1>
  }
};
```



## 예시(&&)

* JSX 안에서, 중괄호를 이용하여 표현식을 포함할 수 있음
  * 값으로 평가되는 식
* 연산자(&&)를 사용하여 엘리먼트를 조건부로 넣기
* 연산자 앞이 true이면 뒤의 JSX 표현식은 출력
  * AND 연산이므로 앞의 표현식에 따라 반환 여부가 결정되므로
* falsy(0과 같은)는 falsy 표현식을 반환

```React
function Header(props) {
  const {isLoggedIn} = props;

  return (
    <div>
    	<h1>안녕하세요. 환영합니다!</h1>
			<!-- 로그인 상태가 아니라면 로그인하는 버튼 표시 -->      
      {!isLoggedIn && <Button>Login</Button>}
    </div>
  );
};
```



## 예시(삼항연산자)

```React
function Header(props) {
  const {isLoggedIn} = props;
  
	return (
  	<h1>
      환영합니다! 지금은 {isLoggedIn? '로그인하셨습니다.' : '로그인을 하셔야합니다.'}
    </h1>
  );
};
```



# Reference

[React 공식 문서](https://ko.reactjs.org/)

