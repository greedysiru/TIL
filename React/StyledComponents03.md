# Styled Components(3) - Themes, createGlobalStyle

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. Themes

* 모든 색상을 가지고 있는 object
* 프로젝트에 일관성 있는 스타일을 정의할 수 있음
* 라이트모드/다크모드를 도입할 수 있음



### Themes 주입

* 가장 상위의 컴포넌트에서 테마를 주입하기
* styled-components의 ThemeProvider를 import

```React
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { ThemeProvider } from 'styled-components';

// 색상을 가지고 있는 object
const theme = {
  textColor: "whiteSmoke",
  backgroundColor: "#111"
};

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <!-- theme 주입 -->
    <ThemeProvider theme={theme}>
      <App />
    </ThemeProvider>
  </React.StrictMode>
);
```



### Themes 사용

* 주입된 theme는 각 styled-component에서 props로 접근 가능

```React
import styled, {keyframes} from 'styled-components';

const Text = styled.span`
  color: ${(props) => props.theme.textColor}
	font-size: 32px;
`;

const Square = styled.div`
	display: flex;
	justify-content: center;
	align-items: center;
  width: 50vw;
  height: 50vh;
	background-color: ${(props) => props.theme.backgroundColor};
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



## 2. createGlobalStyle

* 전역 스코프의 스타일을 적용하는 styled component
  * css Reset을 적용
  * 폰트 등을 정의

```React
const GlobalStyle = createGlobalStyle`
  // 전역 스타일 정의
`;
```





# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

