# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (5) (2021.3.22)

# 1. State관리

## 1.1 단방향 데이터 흐름

* 데이터는 위에서 아래로, 부모에서 자식으로 넘겨야 한다.
* 라이플 사이클을 고려하면 부모 컴포넌트가 자식 컴포넌트의 props를 받으면 무한 렌더링을 하게 될 것이다.



## 1.2 setState()

* 클래스형 컴포넌트의 state를 업데이트할 때 사용하는 함수
* state가 변경되면 컴포넌트는 리렌더링된다.
* **this.state: 렌더링된 값**



### 예시

```react
import React from "react";

class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      count: 3, // state
    };
  }

  componentDidMount() {}

  addNemo = () => {
    // this.setState로 count를 하나 더하기
    this.setState({ count: this.state.count + 1 });
  };

  removeNemo = () => {
    // 0보다 클때만 명령 실행
    if (this.state.count > 0) {
      // this.setState로 count를 하나 빼기
      this.setState({ count: this.state.count - 1 });
    }else{
      // 0과 같아지면 경고창 출력
      window.alert('네모가 없습니다.');
    }
  };

  render() {
    // 배열 만들기
    // Array.from()은 배열을 만들고 초기화하는 내장 함수
    // Array.from()의 첫번째 파라미터로 {length: 원하는 길이} 객체를,
    // 두번째 파라미터로 원하는 값을 반환하는 콜백함수를 넘겨주면 끝!
    // array의 내장함수 대부분은 콜백 함수에서 (현재값, index넘버)를 인자로 사용
    const nemo_count = Array.from({ length: this.state.count }, (v, i) => i);

    // 숫자가 0부터 순서대로 들어가있다.
    console.log(nemo_count);

    return (
      <div className="App">
        {nemo_count.map((num, idx) => {
          return (
            <div
              key={idx}
              style={{
                width: "150px",
                height: "150px",
                backgroundColor: "#ddd",
                margin: "10px",
              }}
            >
              nemo
            </div>
          );
        })}

        <div>
          {/* 함수를 호출합니다. 이 클래스 안의 addNemo 함수를 불러오기 때문에 this.addNemo로 표기 */}
          <button onClick={this.addNemo}>하나 추가</button>
          <button onClick={this.removeNemo}>하나 빼기</button>
        </div>
      </div>
    );
  }
}

export default App;
```



## 1.3 useState()

* 함수형 컴포넌트에서 state 관리



### 예시

```react
import React from 'react';

const Nemo = (props) => {
  // count에는 state 값, setCount는 count를 수정하는 함수가 된다.
  // useState(초기값)
  const [count, setCount] = React.useState(3);

  const addNemo = () => {
    // setCount로 의해 count에 저장된 값을 +1
    setCount(count + 1);
  }

  const removeNemo = () => {
    // 삼항 연산자로 0보다 큰 경우에만 count - 1
    setCount(count > 0? count - 1 : 0);
  }

  const nemo_count = Array.from({length: count}, (v, i) => (i));
  return (
    <div className="App">
        {nemo_count.map((num, idx) => {
          return  (
            <div key={idx} style={{
              width: '150px',
              height: '150px',
              backgroundColor: '#eee',
              margin: '10px'
            }}>
              nemo
            </div>
          )
        })}
        <button onClick = {addNemo}>하나 추가</button>
        <button onClick = {removeNemo}>하나 빼기</button>
      </div>
  );
}

export default Nemo;
```



# 2. Event listener

* 사용자가 하는 행동을 지켜보는 것
* 엘리먼트에 직접 넣거나 addEventListener를 통해 추가 가능



## 클래스형 컴포넌트에서 envent listener 구독하기

### Ref 만들기

```react
constructor(props) {
    super(props);

    this.state = {
      count: 3,
    };

    // Ref
    this.div = React.createRef();
  }

...

	return (
      <div className="App" ref={this.div}>
        <Nemo/>
      </div>
    );
...
```



### addEventListener 등록

* componentDidMount()에 등록하기

```react
hoverEvent = (e) => {
    if(e.target.className === 'app'){
      // 배경색 바꾸기
      e.target.style.background = "#eee";
    }
  }

  componentDidMount() {
    // 마우스를 올리면 이벤트 발생하도록 addEvnetListener 등록
    this.div.current.addEventListener("mouseover", this.hoverEvent);
  }
```



### 컴포넌트가 사라지면 지워주기

* componentWillUnmount()에서 지워주기

```React
componentWillUnmount() {
    this.div.current.removeEventListener("mouseover", this.hoverEvent);
  }
```



# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)

