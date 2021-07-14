# Hooks, useState, useEffect 정리

## 1. Hooks

* Hooks는 사용하기 위해 react로부터 import 해야한다.
* 함수형 프로그래밍을 할 수 있다.
* **componentDidMount** 에서 이벤트 리스너를 설정, **componentWillUnmount**에서 cleanup 로직을 수행할 때 버그가 쉽게 발생하고 무결성을 해침
  * 개념상 똑같은 effect라도 생명주기 메소드는 이를 분리하게 함
  * 오히려 관련이 없는 로직을 모아 놓음
* Hook을 통해 서로 비슷한 것을 하는 작은 함수의 묶음으로 컴포넌트를 나눈다.
* Class의 **this** 키워드는 혼동을 일으키고 코드 재사용성과 구성을 어렵게 함
  * Hook은 Class없이 React 기능을 사용하는 방법을 제시
* React에서는 기본 내장 Hook을 제공한다.
  * custom hook을 만들기도 가능
* **JavaScript의 클로저를 이용하여 리액트에 한정된 API를 고안하기보다 JavaScript가 이미 가지고 있는 방법을 이용하여 문제를 해결**
* **React는 Hook이 호출되는 순서에 의존**한다.
  * 모든 렌더링에서 Hook 호출 순서는 같다.



### Hook 사용 규칙

* 최상위(at the top level)에서만 호출
  * 반복문, 조건문, 중첩된 함수 내에서 실행하지 말 것
  * Hook 호출 순서가 밀려나면 버그가 발생
* function component 내에서만 Hook을 호출
* 린트 규칙으로 강제할 수 있다.

## 2. useState

> **const [item, setItem] = useState(initial state);**

* f**unction component**에서 **state**와 **lifecycle features**를 연동할 수 있다.

* 현재의 state값과 state를 업데이트 하는 함수를 쌍으로 제공(array)

  * 배열 구조 분해로 각각을 받아올 수 있다.

* **class component**에서 **this.setState**와 유사

  * **this.state** 는 객체지만, Hook의 state는 객체일 필요가 없음

* 여러 개를 사용할 수 있다.

  



### 예시

```React
import React, { useState } from "react";

...

const App = () => {
  // count의 초기값은 0, setCount로 count를 바꿀 수 있다.
  const [count, setCount] = useState(0);
  // setCount를 이용하여 count에 1을 더하는 함수
  const incrementCount = () => setCount(count + 1);
  return (
  	<>
    	<h1>{count}</h1>
      // button에 onClick 이벤트가 일어나면 state의 count가 1 증가한다.
    	<button onClick = {setCount}> up to count </button>
    </>
  );
};

```



## 3. useEffect

> **useEffect(( ) => {**
>
> ​	**함수**
>
> **}, [dependency])**

* **function component** 안에서 **side effects**를 수행할 수 있게 한다.

  * side effects: 컴포넌트 안에서 데이터를 가져오거나 구독, DOM을 직접 조작하는 것
  * **class component**의 **componentWillUnmount, componentDidMount, componentDidUpdate**를 하나의 API로 통합

* **useEffect** 를 사용하면 React는 DOM을 바꾼 후 **effect** 함수를 실행

  * 렌더링 이후, 어떤 일을 수행

* 두개의 인자를 받는다

  * 첫번째 인자: useEffect가 실행되면 실행할 함수
  * **두번째 인자: dependency(array)**
  * **deps**가 있다면, **useEffect는 deps 리스트에 있는 값일 때만 값이 변하도록 활성화**
  * **빈 배열**을 전달하면 **component가 mount되었을 때만 실행**

* 기본적으로 첫번째 렌더링과 이후의 모든 업데이트에서 수행

  * Component가 화면에 나왔을 때 또는 새로고침 하였을 때 -> componentDidMount -> useEffect 실행
  * state가 업데이트 되엇을 때 -> componentDidUpdate -> useEffect 실행

* **effect**를 해제하려면 **return**으로 반환한다.

  * component가 unmount될 때 해제된다.

* 컴포넌트 내에서 여러 개의 **useEffect** 사용 가능

* **useEffect** 에서 사용되는 effect는 브라우저가 화면을 업데이트하는 것을 차단하지 않는다.

  * 애플리케이션의 반응성 향상
  * 비동기적으로 실행
  * **useLayoutEffect**: **useEffect** 와 동일한 API를 사용하며 동기적으로 실행

  

### side effects , 정리가 필요하지 않은 것 vs. 정리가 필요한 것

| 정리가 필요하지 않은 것                    | 정리가 필요한 것                      |
| ------------------------------------------ | ------------------------------------- |
| 네트워크 요청<br />DOM 수동 조작<br />로깅 | 외부 데이터에 구독(subscription) 설정 |

* 정리 (clean up)를 해야하는 이유?
  * 메모리 누수가 발생하지 않도록 하기 위해서
  * class에서는 **componentDidMount** 에서 구독, **componentWillUnmount** 에서 정리.

### 예시

```React
import React, { useState , useEffect } from "react";

...

const App = () => {
  const effect = () => console.log('use effect');
  useEffect(() => {
    // compoenent가 mount 된 뒤, 문구가 출력된다. (componentDidMount)
    effect();
  })
  const [count, setCount] = useState(0);
  const incrementCount = () => setCount(count + 1);
  return (
  	<>
    	<h1>{count}</h1>
      // button을 눌렀을 때, state의 카운트가 올라가며 useEffect의 effect함수도 실행되어 문구가 출력(componentDidUpdate)
    	<button onClick = {setCount}> up to count </button>
    </>
  );
};
```



### deps를 입력했을 때 예시

```React
import React, { useState , useEffect } from "react";

...

const App = () => {
  const effect = () => console.log('use effect');
  const [count, setCount] = useState(0);
  const [countTwo ,setCountTwo] = useState(0);
    useEffect(() => {
    // compoenent가 mount 된 뒤, 문구가 출력된다. (componentDidMount)
    effect();
  }, [count])
  const incrementCount = () => setCount(count + 1);
  const incrementCountTwo = () => setCountTwo(countTwo + 1);
  return (
  	<>
    	<h1>{count}</h1>
      // setCount가 실행될 때만 count가 증가하므로 이때만 문구가 출력된다. (componentDidUpdate)
    	<button onClick = {setCount}> up to count </button>
   	 <button onClick = {setCountTwo}> up to countTwo </button>
    </>
  );
};
```



### Effect 해제(clean up)

* **class component**

```React
...
componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
// 개념상 똑같은 subscribToFriendStatus와 unsubscribToFriendStatus가 생명주기 메소드로 인해 분리
...
```



* **useEffect(function component)**

```React
...
  useEffect(() => {
    // 친구의 접속 상태를 구독하는 effet
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // 구독을 해지
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
...
```

effect가 정리되는 시점은 컴포넌트가 마운트 해제되는 때이다. effect는 렌더링이 실행될 때마다 실행되므로 다음차례의 effect를 실행하기 전에 이전의 렌더링에서 파생된 effect를 정리해야 한다.



### Effect가 업데이트 시마다 실행되는 이유

* props가 업데이트 되었을 때, Effect가 실행되지 않는다면 버그가 일어난다. 아래의 코드는 class component의 life cycle 함수를 사용하여 구독, 구독해제하였는데, this.props가 업데이트되어도 화면에 반영되지 않는다. 

```React
 ...
componentDidMount() {
   // 구독
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    // 구독해제
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
...
```

</br>

* 그러므로 **componentDidUpdate** 를 사용하여 반영되도록 아래처럼 추가한다.

```React
componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate(prevProps) {
    // 이전 friend.id에서 구독을 해지
    ChatAPI.unsubscribeFromFriendStatus(
      prevProps.friend.id,
      this.handleStatusChange
    );
    // 다음 friend.id를 구독
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

</br>

* **useEffect** 를 사용하면 기본적으로 업데이트를 다루므로 특별한 코드 없이 간단하게 작성하면 된다. 다음의 effect를 다루기 전에 이전의 effect를 정리하기 때문이다.

 ```React
 ...
   useEffect(() => {
     // 친구의 접속 상태를 구독하는 effet
     ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
     // 구독을 해지
     return () => {
       ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
     };
   });
 ...
 ```



### 성능 최적화 하기

* 렌더링 이후 effect를 정리하는 것이 때때로 성능저하를 일으킴

</br>

* class component의 경우 아래처럼 처리하여 state나 props가 업데이트 되었을 때 최적화를 한다.

```React
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = **You clicked ${this.state.count} times**;
  }
}
```

</br>

* useEffect에서는 두 번째 인수로 배열을 넘긴다.
  * count가 5이고 리렌더링 이후 5라면, effect를 건너뛰어 최적화가 된다.
  * count가 달라지면 effect를 재실행

```React
useEffect(() => {
  document.title = **You clicked ${count} times**;
}, [count]); // count가 바뀔 때만 effect를 재실행
```



## 4. Hook 관련 기타

* effect 외부의 함수 컴포넌트에서 어떤 props, state를 사용하는지 기억하기 어려우므로 **내부의 effect에 필요한 함수 컴포넌트를 선언하는 것이 일반적이다.**

# Reference

[실전형 리액트 Hooks 10개](https://nomadcoders.co/react-hooks-introduction/lobby)

[React 공식 docs - Hook](https://ko.reactjs.org/docs/hooks-intro.html)