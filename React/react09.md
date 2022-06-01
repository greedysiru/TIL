# State와 생명주기(2)



## State를 올바르게 사용하기

### 1. 직접 State를 수정하지 말기

* 클래스형 컴포넌트에서

```JavaScript
// 임의의 메서드
setNewState() {
  // 직접 변경하면, 컴포넌트를 다시 렌더링하지 않음
  this.state.text = '변경';
}

// 아래와 같이 setState를 사용할 것
setNewState() {
  this.setState({text: '변경'});
}

// constructor
constructor(props) {
  super(props);
  // 직접 state를 지정할 수 있는 곳은 constructor가 유일
  this.state.text = '초기값';
}


```



### 2. State 업데이트는 비동기적일 수 있음

* 여러 setState 호출을 단일 업데이트로 일괄 처리 가능
* props와 state는 비동기적으로 업데이트될 수 있음
* setState에서 콜백을 사용하여 이를 방지

```JavaScript
this.setState((state, props) => {
	counter: state.counter + props.increment
})
```



### 3. State 업데이트는 병합됨

* State에 포함된 변수들을 각각 업데이트 가능
* 병합은 얕게 이루어짐

```JavaScript
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      text: '',
      userName: '',
    };
  };
  
  componentDidMount() {
    // text를 받아오는 api 요청 함수
    fetchHeaderText().then(response => {
      // state의 text만 업데이트
      this.setState({
        text: response.text
      });
    });
    
    // userName을 받아오는 api 요청함수
    fetchUserName().then(response => {
      this.setState({
        // state의 userName만 업데이트
        userName: response.userName
      })
    })
  }
  
}
```



### 4. 데이터는 아래로 흐름

* 다른 컴포넌트는 특정 컴포넌트가 어떤 상태를 가지는지 알 수 없음
  * **state는 캡슐화되어 있기 때문**
  * state를 소유한 컴포넌트를 제외한 다른 컴포넌트에서 해당 state에 접근할 수 없음
* 컴포넌트는 자신의 state를 자식 컴포넌트에 props로 전달할 수 있음
  * 하향식(top-down) 또는 단방향식 데이터 흐름이라고 함
* 모든 state는 특정한 컴포넌트가 소유하고 있음
* state로부터 파생된 UI 또는 데이터는 오직 아래에 있는 컴포넌트에만 영향을 미침5



# Reference

[React 공식 문서](https://ko.reactjs.org/)

