# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (6) (2021.3.22)



# 1. 라우팅

## 1.1 SPA

* Single Page Application
* html이 1개인 어플리케이션
* 전통적인 웹 사이트: 페이지를 이동할 때마다 서버에서 html, css, js (=정적자원)을 내려준다.
  * 페이지를 이동할 때마다 서버에서 주는 방식은 화면을 바꿀 때의 상태유지가 어렵고 바뀌지 않은 부분까지 새로 불러와 비효율적이다.
* SPA: 딱 한번만 정적자원을 받는다.
* 장점: 사용성
* 단점
  * 처음에 모든 컴포넌트를 받아온다.
  * 사용자가 들어가지 않는 페이지까지 전부 가지고 온다.
  * 첫 로딩속도가 느리다.



## 1.2 라우팅

* 브라우저의 주소에 따라 다른 페이지를 보여주는 것
* SPA에서는 라우팅 라이브러리를 사용하여 구현



# 2. 라우팅 라이브러리

## 2.1 react-route-dom 패키지

```shell
yarn add react-router-dom
```

* [공식 문서](https://reactrouter.com/web/guides/primary-components)



## 2.2 리액트에서 라우팅 처리

### index.js에 BrowserRouter 적용

* index.js: index.html에 있는 div#root에 컴포넌트를 실제로 랜더링하도록 연결

* **BrowserRouter**: 웹 브라우저가 가지고 있는 주소 관련 정보를 props로 넘겨준다.
  * 현재 클라이언트가 어느 주소를 보고 있는 지 쉽게 알 수 있게 도와준다.

```react
import React from 'react';
import ReactDOM from "react-dom";
// 라우터 import
import { BrowserRouter } from "react-router-dom";
import App from './App';

// index.html에 있는 div#root에 우리가 만든 컴포넌트를 실제로 랜더링하도록 연결해주는 부분
ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
```



### App.js에서 Route 적용

* 넘겨줄 props가 없을 때

```react
<Route path="주소[/home 처럼 /와 주소를 적기]" component={[보여줄 컴포넌트]}/>
```

* 넘겨줄 props가 있을 때

```react
<Route path="주소[/home 처럼 /와 주소를 적기]" render={(props) => (<BucketList list={this.state.list} />)} />
```

* 적용 예시

```react
import React from 'react';
import logo from './logo.svg';
import './App.css';
// Route
import { Route } from "react-router-dom";

// 세부 페이지가 되어줄 컴포넌트들 import
import Home from "./Home";
import Cat from "./Cat";
import Dog from "./Dog";

class App extends React.Component {

  constructor(props){
    super(props);
    this.state={};
  }
  
  render(){
    return (
      <div className="App">
        {/* 컴포넌트에 라우트 적용 */}
        <Route path="/" exact component={Home} />
        <Route path="/cat" component={Cat} />
        <Route path="/dog" component={Dog} />
      </div>
    );
  }
}

export default App;
```

`exact`: home 컴포넌트(주소가 /)가 포함되어도 제외한다.



## 2.3 URL 파라미터

> **파라미터: /cat/siru**
>
> **쿼리: /cat?name=siru**



### 파라미터 주기

```react
// App.js
...
<Route path="/cat/:cat_name" component={cat}/>
...
```



### 파라미터 사용

```react
// Cat.js
import React from 'react';

const Cat = (props) => {
  console.log(props.match);
  
  return (
  	<div>고양이 컴포넌트 입니다.</div>
  )
  
}

export default Cat;
```

* /cat/siru로 이동하면 콘솔에 파라미터가 아래처럼 출력
  * params: {cat_name: "siru"}
  * path: "/cat/:cat_name"
  * url: "/cat/siru"



## 2.4 Link 사용하기

```react
<Link to="주소">[텍스트]</Link>
```

### Link 적용

* Route 밖에 있는 돔요소는 페이지가 전환되어도 그대로 유지된다.

```react
// App.js 적용
render(){
    return (
      <div className="App">
        <div>
          {/* Link to를 사용한 네비게이터 */}
          <Link to="/">Home으로 가기</Link>
          <Link to="/cat">Cat으로 가기</Link>
          <Link to="/dog">Dog으로 가기</Link>
        </div>

        <hr />
        {/* 라우트 */}
        <Route path="/" exact component={Home} />
        <Route path="/cat" component={Cat} />
        <Route path="/dog" component={Dog} />
      </div>
    );
  }
```



## 2.5 history 사용하기

* 함수를 사용한 페이지 전환 방법

### import 하기

```react
// import
import {withRouter} from "react-router";
...
// exprot 에서도 아래와 같이 바꿔준다.
export default withRouter(App);
```



### push()

* 이동할 주소로 페이지 이동

```react
this.props.history.push([이동할 주소]);
```



### goBack()

* 뒤로가기

```react
this.props.history.goBack();
```



### history 적용

```react
// App.js
<button onClick={() => {
    // props에 있는 history를 사용
    // push([이동할 주소])는 페이지를 이동
    this.props.history.push('/cat');
  }}>
  /cat으로 가기
</button>
<button onClick={()=>{
    // goBack()은 뒤로가기
    this.props.history.goBack();
  }}>뒤로가기
</button>
```



## 2.6 잘못된 주소 처리

* 정하지 않은 주소로 들어온 경우 처리하는 방법



### 빈 컴포넌트 만들기

```react
import React from 'react';

const NotFound = (props) => {
  return <h1>올바르지 않은 주소입니다.</h1>;
};

export default NotFound;
```



### Switch 추가하기

```react
// App.js
import NotFound from './NotFound';
...
// Switch import
import { Route, Switch } from "react-router-dom";
...
class App extends React.Component {
  ...
  render() {
    return (
      <div className="App">
        ...
          <Switch>
            <Route
              path="/"
              exact
              render={(props) => (
                <BucketList
                  list={this.state.list}
                  history={this.props.history}
                />
              )}
            />
            <Route path="/detail" component={Detail} />
            {/* 없는 주소인 경우 path가 정의되어있지 않은 컴포넌트가 나오게 된다. */}
            <Route component={NotFound} />
          </Switch>
        ...
      </div>
    );
  }
}
...
```





# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)

[react-route-dom 공식 문서](https://reactrouter.com/web/guides/primary-components)

