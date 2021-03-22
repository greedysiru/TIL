# [항해99 1기] [Chapter3-1] 주특기 기본 - 프론트의 꽃 리액트 (3) (2021.3.21)



# 1. Component

> **리액트가 레고라면 컴포넌트는 블록이다.**

* 웹 사이트의 조각이라고 할 수 있다.
* 클래스형과 함수형이 있다.



## 1.1 State와 Props

* Component에서의 **데이터 관리**
* **State**
  * Component가 가지고 있는 데이터
  * 한 Component에서만 사용하는 정보를 주로 넣고 생성, 수정하는 데이터
  * 생성, 수정은 오직 해당 Component에서만 이뤄진다.
* **Props**
  * Component가 부모 Component로부터 받아온 데이터
  * 부모로부터 받아온 것이므로 수정할 수 없다.



## 1.2 함수형 Component

* 리액트에서 폴더는 소문자로 시작하는 카멜케이스, JS파일, 컴포넌트 이름은 대문자로 시작하는 카멜케이스를 사용한다.

### 함수형 컴포넌트 예시

```react
// 리액트 패키지 불러오기
import React from 'react';

// 함수형 컴포넌트
// props: 부모 컴포넌트에게 받아온 데이터
const BucketList = (props) => {
  // 컴포넌트가 보여줄 ui 요소(react element)
  return (
  	<div>
    	버킷 리스트
    </div>
  );
}

// 만든 컴포넌트를 사용하기 위해서 export
// 다른 컴포넌트에서 import하여 해당 컴포넌트를 사용할 수 있다.
export default BucketList;
```



### 부모 컴포넌트에서 가져오기

```react
import React from 'react';
import BucketList from './BucketList';

function App() {
  return (
  	<div className="App">
    	<h1>내 버킷리스트</h1>
      {/* 가져온 컴포넌트 넣기 */}
      <BucketList/>
    </div>
  
  );  
}

export default App;
```



## 1.3 클래스형 Component

### 클래스형 컴포넌트 예시

* 위의 부모 컴포넌트를 클래스형으로 바꾼 예시

```react
import React from 'react';
import BucketList from './BucketList';

// 클래스형 컴포넌트
class App extends React.Component {
  constructor(props){
    super(props);
    // App 컴포넌트의 state 정의
    this.state = {
      list: ['영화관 가기', '매일 책읽기', '수영 배우기'],
    };
  }
  
  // 렌더 함수 안에 리액트 앨리먼트 넣기
  render() {
    return(
    <div className="App">
      <h1>내 버킷리스트</h1>
        {/* 컴포넌트 */}
      	<BucketList/>
    </div>
    );
  }
}

export default App;
```



## 1.4 Component 간 데이터 넘기기

* 부모 컴포넌트가 가진 state를 자식 컴포넌트에 넘길 수 있다.
* 함수형 컴포넌트에는 state가 없다.
  * React hook을 사용하면 함수형 컴포넌트에서도 사용할 수 있다.
* 컴포넌트 넘기기

```react
< 컴포넌트 명 [props 명] = {넘겨줄 것 (리스트, 문자열, 숫자, ...)}/ >
```



### 부모 컴포넌트에서 자식 컴포넌트로 state 넘기기

```react
render() {
  return (
  // this 키워드로 state 접근
  <div className="App">
      <h1>내 버킷리스트</h1>
      {/* 컴포넌트 */}
      
    	<BucketList list={this.state.list}/>    
  </div>  
  );  
}
```



# 2. React에서 CSS 사용하기

* 스타일을 설정한 별도의 CSS 파일을 만들고 import할 수 있다.

```react
import React from 'react';
import BucketList from './BucketList';
// CSS 파일 경로
import './style.css';
```



# Reference

[스파르타코딩클럽 - 프론트엔드의 꽃 리액트](https://spartacodingclub.kr/online/react)

