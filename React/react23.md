# Hook의 개요

* Hook은 하위 호환성을 가지고 있음



## 1. useState

* useState는 현재의 state 값과 업데이트하는 함수를 쌍으로 return
* 이전 state와 새로운 state를 합치지 않음
  * 새로운 state로 대체
* 인자로 state 값 하나를 받음
* **React state와 생명주기 기능을 연동할 수 있게하는 함수**

```React
import React, {useState} from 'react';

function Header() {
  const [text, setText] = useState('헤더입니다.');
  
  return <h1>{text}</h1>
}
```



## 2. vs. Class 컴포넌트의 setState

### 선언 방법

```React
// Class Component
class Header extends React.component {
  constructor(props) {
    super(props);
    this.state = {
      text: '헤더입니다.'
    };
  }
}

// Functional Component
function Header (props) {
  const [text, setText] = useState('헤더입니다.');
}
```



### state 사용

```React
// Class Component
<h1>{this.state.text}</h1>

// Functional Component
<h1>{text}</h1>
```



### state 갱신

```React
// Class Component
<button onClick={() => this.setState({text: '헤더입니다2.'})}>텍스트 변경</button>

// Functional Component
<button onClick={() => setText('헤더입니다2.')}>텍스트 변경</button>
```

# Reference

[React 공식 문서](https://ko.reactjs.org/)

