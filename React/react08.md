# State와 생명주기(1)



## State

* 클래스형 컴포넌트에서 state 정의하기

```React
class Header extends React.Component {
  constructor(props) {
    // props를 인스턴스에 전달
    // 클래스 컴포넌트는 항상 props로 constructor를 호출해야 함
    super(props);
    this.state = {text: '헤더 컴포넌트 입니다.'};
  }
  
  render() {
    return <h1>{this.state.text}</h1>;
  };
}
```



## 생명주기 메서드

* 마운팅 : 컴포넌트가 DOM에 렌더링되는 시점
* 언마운팅 : 컴포넌트가 DOM에서 삭제되는 시점
* 컴포넌트 클래스에서 생명주기 메서드를 선언하여, 마운트와 언마운트 시점에서 특정 코드를 실행시킬 수 있음



### 예시

```React
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {text: '헤더 컴포넌트 입니다.', nowHours: ''};
  }
  
  // 컴포넌트가 DOM에 렌더링 된 후에 실행
  componentDidMount() {
    this.timerID = setInterval(
      // 1초마다 이 컴포넌트에서 정의된 getNowHours 메서드 실행
    	() => this.getNowHours(),
      1000
    );
  }
  
  // 컴포넌트가 DOM에서 삭제 된 후에 실행
  componentWillUnmount() {
   clearInterval(this.timerID);
  }
  
  // 컴포넌트의 메서드
  // 현재 시간 정보를 가져오기
  getNowHours() {
    this.setState({
      nowHours: new Date().getHours();
    })
  }
  
  render() {
    return (
      <div>
      	<h1>{this.state.text}</h1>
        <h2>현재 시각은 {this.state.nowHours}입니다.</h2>
      </div>
    );
  };
}

ReactDOM.render(
  <Header />,
  document.getElementById('root')
);
```



### 예시 코드의 실행 순서

1. Header 컴포넌트가 ReactDOM.render에 전달 되면, 리액트는 컴포넌트의 constructor를 호출
   - 이 시점의 this.state.nowHours는 빈 문자열
2. 리액트는 Header 컴포넌트의 render 메서드를 호출하고 컴포넌트의 출력값을 일치시키기 위해 DOM을 업데이트
3. 컴포넌트의 출력값이 DOM에 삽입되면, 리액트는 componentDidMount 메서드 호출 됨. 이 때, 컴포넌트타이머를 설정하도록 브라우저에 요청
4. 브라우저가 getNowHours 메서드를 호출. setState에 nowHours를 현재 시각으로 최신화. **이 때 리액트는 state가 변경된 것을 인지하여, render메서드를 재호출. this.state.nowHours가 달라지고 렌더링 출력값은 업데이트된 값을 포함. 리액트는 이에따라 DOM 업데이트**
5. 컴포넌트가 삭제되면, componentWillUnmount 메서드 실행

# Reference

[React 공식 문서](https://ko.reactjs.org/)