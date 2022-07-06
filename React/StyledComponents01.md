# Styled Components(1) - 개요, 스타일링 방법, 동적 스타일링, 컴포넌트 확장

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. Styled Components

* React.js에서 최적화된 스타일링 제공
* **CSS를 살펴보지 않고도 각각의 컴포넌트가 맡은 일을 파악할 수 있음**
  * 컴포넌트에 사용되는 각 요소에대해서 역할에 따른 이름을 붙여줄 수 있어, 코드 파악에 용이
  * Styled Components가 해당 요소에 독자적인 class명을 붙여줌
* 컴포넌트의 확장
  * 기존의 컴포넌트 스타일을 확장할 수 있음
* 동적 스타일링
  * props를 활용하여 컴포넌트 스타일링할 수 있음



## 2. 스타일링 방법

```React
import styled from 'styled-components';


const Header = styled.h1`
  color: white;
`;


function App() {
  return <Header>헤더입니다.</Header>
}

export default App;
```



## 3. 동적 스타일링

* props로 스타일의 속성 값을 넘겨받아 동적으로 스타일링 가능

```React
import styled from 'styled-components';


const Text = styled.h1`
  color: ${(props) => props.textColor} ;
`;


function App() {
  return (
    <>
    	<Text textColor="white">텍스트입니다.</Text>
	    <Text textColor="teal">텍스트입니다.</Text>
  	</>
  )
}

export default App;
```



## 4. 컴포넌트 확장

* 기존에 정의한 컴포넌트를 확장할 수 있음

```React
import styled from 'styled-components';


const Text = styled.span`
  color: ${(props) => props.textColor} ;
`;

const Header = styled(Text)`
	font-size: 30px;
`;


function App() {
  return (
    <>
    	<Header textColor="white">헤더입니다.</Text>
	    <Text textColor="teal">텍스트입니다.</Text>
  	</>
  )
}

export default App;
```



# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

