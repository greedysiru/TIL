# Effect Hook 사용하기(1)



## 1. useEffect의 역할

* 함수 컴포넌트에서 side effect를 수행
* side effect
  * 데이터 가져오기(API 호출)
  * 구독 설정하기
  * 수동으로 React 컴포넌트 DOM을 수정
  * 정리(Clean-up)가 필요한 것, 필요하지 않은 것 두 종류가 있음
* useEffect는
  * class 생명주기의 componentDidMount + componentDidUpdate + componentWillUnmoun를 합친 것으로 보아도 됨
* React Component가 렌더링되기 전에는 side effect를 실행하지 않음
  * why? 이 시점은 이른 시기로서 React가 DOM을 업데이트하고 난 이후에 실행해야 함



## 2. useEffect가 하는 일

* **React에게 컴포넌트가 렌더링된 이후에 어떤 일을 수행해야하는 지를 말함**
  * DOM 업데이트를 수행한 이후에 side effect를 수행
* **렌더링, 리렌더링을 할 때마다 전달되는 side effect 함수는 매번 교체되어 전달됨**
* 컴포넌트 안(함수 내)에서 불러내어 state, props에 접근할 수 있음
* 기본적으로 렌더링이 될 때마다 수행(첫 렌더링 및 모든 업데이트)



## 3. useEffect vs. Class Component Life Cylce Methods

* useEffect는 기본적으로 컴포넌트가 렌더링 또는 모든 업데이트가 일어날 때마다 실행됨
* Class Component에서 componentDidMount는 컴포넌트가 렌(더링 되었을 때, componentDidUpdate는 컴포넌트가 업데이트 되었을 때 실행 됨
* 컴포넌트가 렌더링(리렌더링 포함)될 때마다 실행해야하는 코드가 있을 경우, useEffect를 사용하는 것이 더 효율적으로 side effect를 실행할 수 있음
* class component는 렌더링, 리렌더링 시점의 Life Cycle Methods가 분리되어 있어 중복 코드가 발생

```React
// Class Compnent
class ClassComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      renderCount: 0
    }
  }
  
  // 첫 렌더링 시점 side effect 호출
  componentDidMount() {
    console.log(`이 컴포넌트는 ${this.state.renderCount}번 렌더링 되었습니다.`);
  }
  // 재 렌더링 시점 side effect 호출
  componentDidUpdate() {
    console.log(`이 컴포넌트는 ${this.state.renderCount}번 렌더링 되었습니다.`);
  }
  
  render() {
    return (
    <div>
    	<button onClick={() => this.setState({count: this.state.count + 1})}  >
       재 렌더링 실행
      </button>
    </div>
    )
  }
}

// Functional Component
function FunctionalComponent() {
  const [renderState, setRenderState] = useState(0);
  
  // 첫 렌더링, 재 렌더링 시점 side effect 호출
  useEffect(() => {
    console.log(`이 컴포넌트는 ${this.state.renderCount}번 렌더링 되었습니다.`);
  });
  
  return (
    <div>
      <button onClick={() => this.setState({count: this.state.count + 1})}  >
        재 렌더링 실행
      </button>
    </div>
  )
}
```



## 4. 정리 및 느낀점

React로 구현하는 프로젝트에서 가장 많이 사용되는 Hook을 꼽자면, 단언컨테 useState와 useEffect라고 할 수 있다.
현업에서 useEffect의 주된 용도는 API를 호출하는 것이었다. API 호출은 async로 이루어져야 하는데, Promise 객체를 return하게 된다. 그러므로 useEffect의 callback으로서 바로 async를 줄 수는 없다. 왜냐하면, useEffect의 callback은 undefined(아무 것도 return 안함)나 clean up을 return해야하기 때문이다.
그러므로, API를 async 함수로 호출하기 위해 아래 예시와 같이 useEffect 내부에서 정의하고 호출하면 된다. 단, 아래의 코드는 Dependancy Array가 명시되어 있지 않아 useEffect의 기본 동작대로 모든 렌더링에서 side effect로서 api를 호출하게 된다.

```React
useEffect(() => {
	const fetchAPI async () => {
    const result = await fetch('url');
    ...
  }
	fetchAPI();
})
```



# Reference

[React 공식 문서](https://ko.reactjs.org/)

