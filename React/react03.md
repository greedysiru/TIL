# [노마드 코더] 리액트 Hooks 10분만에 사용법 배우기

**상세 내용 [블로그](https://greedysiru.tistory.com/601) 참고**

# 1. Hooks?

* functional component에서 state를 가질 수 있게 한다.
* 앱을 리액트 훅으로 만든다면, class component, did mount, render 등을 안해도 된다.
* functional programming 스타일로 작성할 수 있다.
* 사용할 hooks를 react로부터 import하여 사용한다.



# 2. useState

### class component의 state 관리 vs.  function component의 state 관리 (useState)

* class Component

```React
...

class App extends Component {
  state = {
    count: 0
  }

	modify = (n) => {
    this.setState({
      count:n
    });
  };
	
  render() {
    const {count} = this.state;
    return (
      <>
    <div>{count}</div>
    <button onClick={() => this.modify(count + 1)}>Increment</button>
      </>
    );
  }
}

...
```



* function component

```React
...

const App = () => {
  const [count, setCount] = useState(0);
  return (
  	<>
    	{count}
    <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  )
}

...
```



### useState

> **const [value, 변경하는 방법] = useState(초기값);**

* useStater가 array를 return
* 변경하는 방법은 보동 동사형으로 작명



# 3. useEffect

* Class Component의 componentDidMount, componentDidUpdate와 비슷한 역할
* API에서 데이터를 요청할 때 사용



# Reference

[리액트 Hooks 10분만에 사용법 배우기](https://www.youtube.com/watch?v=yS-BU6eYUDE&t=609s)

[React 공식 docs](https://ko.reactjs.org/docs/hooks-intro.html)