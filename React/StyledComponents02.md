# Styled Components(2)

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. as

* 명시된 HTML 요소 말고 다른 HTML 요소를 사용하는 기능

```React
import styled from 'styled-components';


const Text = styled.text`
  color: white;
`;


function App() {
  // Text 컴포넌트는 text 요소로 지정되어있어도 as를 사용하여 h1 태그로 사용 가능
  return <Text as="h1" >헤더입니다.</Text>
}

export default App;
```



## 2. Attrs

* HTML Attributes에 접근 가능

```React
import styled from 'styled-components';


const Btn = styled.button.attrs({ disabled: true, })`
  color: white;
  background-color: tomato;
`;


function App() {
  return <Btn>비활성화된 버튼</Btn>
}

export default App;
```



## 3. Animations

* styled-components의 keyframes을 import
* 변수에 애니메이션을 정의할 수 있음
* 정의한 애니메이션을 템플릿 리터럴로 컴포넌트에 적용할 수 있음

```React
import styled, {keyframes} from 'styled-components';

// 애니메이션 정의
const rotationAnimation = keyframes`
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
`;

// 정의한 애니메이션을 템플릿 리터럴로 적용
const Square = styled.div`
	background-color: teal;
	animation: ${rotationAnimation} 1s linear infinite;
`;

function App() {
  return <Square>
}

export default App;
```



## 4. selector

* styled-components 로 정의한 컴포넌트 안에 HTML 태그명을 선택자로 사용할 수 있음

```React
import styled from 'styled-components';

const Square = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
	background-color: teal;

	span {
		color: white;
	}
`;

function App() {
  return (
    <Square>
      <span>각진 컴포넌트</span>
    </Square>
  );
}

export default App;
```



## 5. Pseudo Selector

* 의사 클래스
* 선택자에 추가하는 키워드
* 선택한 요소가 특별한 상태일때 만족
  * styled component가 특정 상태일 때 가질 스타일도 정의할 수 있음
* styled-components에서는 (&)으로 축약하여 표현 가능

```React
import styled from 'styled-components';

const Text = styled.span`
	font-size: 32px;
`;

const Square = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
	background-color: teal;
	${Text} {
		color: white;
		&:hover {
			color: teal;
		}
	}
`;

function App() {
  return (
    <Square>
      <Text>각진 컴포넌트</Text>
    </Square>
  );
}

export default App;
```



# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

