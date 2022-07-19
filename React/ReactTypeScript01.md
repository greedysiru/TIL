# React & TypeScript

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. Prop Types vs. TypeScript

* Prop Types는 prop이 컴포넌트에 전달되었는지 **런타임에서 확인(콘솔)**
* TypeScript는 **런타임 이전에 prop이 컴포넌트에 전달되었는지 확인**
* 즉, TypeScript가 더 강력하게 오류를 방지할 수 있음



## 2. interface

* object shape를 TypeScript에게 설명
* 강력한 타입검사 지원
* IDE 자동완성 지원

```React
import styled from 'styled-components';

const Container = styled.div<TextProps>`
	font-size: 34px;
	color: ${(props) => props.color};
	bold: ${(props) => props.bold ? 700 : 400};
`;

interface TextProps {
  color: string;
  bold?: boolean;
};

function Text({color, bold}: TextProps) {
  return <Container color={color} bold />
}

export default Text;
```



## 3. event & TypeScript

* event 핸들러를 사용할 때 전달되는 event의 타입을 지정할 수 있음
  * Documents나 구글링을 통해 적용할 것
* 리액트 내에서의 이벤트는 자바스크립트의 실제 이벤트가 아닌, SyntheticEvent를 넘기는 것임
  * [SyntheticEvent](https://reactjs.org/docs/events.html) 참고



### React.FormEvent

* React.FromEvent: Form 태그 내에서 일어나는 이벤트
* 제네릭으로 넘기는 것은 어떤 종류의 Element가 이벤트를 발생시킬지를 특정

```React

import React, {useState} from 'react';

function App() {
  const [value, setValue] = useState("");
  // React.FormEvent: 이벤트에대한 타입 
  // 제네릭으로 넘기는 것은 어떤 종류의 Element가 onChange 이벤트를 발생시킬지를 특정
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    const {currentTarget: {value}} = event;
    setValue(value);
  };

  return (<div>
    <form onSubmit={onSubmit}>
      <input value={value} onChange={onChange} type="text" placeholder="username"/>
    </form>
    </div>);
}

export default App;
```



# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

