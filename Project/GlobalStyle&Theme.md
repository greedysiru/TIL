

# styled-components를 활용한 전역 스타일링과 테마

## 서론

현재 근무하고 있는 회사의 프론트엔드 소스코드에서 스타일링은 대부분 SCSS로 정의되어 있다. 이는 과거 퍼블리셔가 있던 흔적으로, 퍼블리셔가 마크다운과 스타일링을 하여 프론트엔드에게 넘겨주고 이를 받아 마크다운은 React JSX로 마이그레이션하고 SCSS로 스타일링을 하였다고 들었다.
하지만, 퍼블리셔가 없고 프론트 엔지니어만 있는 현재, 이 방식은 대단히 불편하다. React에서 컴포넌트 정의와 스타일링을 JS와 SCSS를 오가며 해야하는 것이 비효율적이라고 생각하기 때문이다. 또, 컴포넌트 스코프에만 스타일 시트를 적용하기 위해 classnames라는 라이브리를 사용해야 하는데 아래와 같이 보일러 플레이트가 많이 발생하는 것도 좋지 않았다.

```React
import classnames from 'classnames/bind';
import style from './ViewStyle.scss';
...

const cx = classnames.bind(style);
function View() {
	return (
		<div className={cx('layout'}></div>
	)
}
```

이러한 문제점을 타파하고자, CSS-in-JS로 스타일링을 해야겠다고 결심하였고 styeld-component를 사용하기로 팀원들과 이야기하여 결정했다.





## 1. styled-component 도입 이유

도입 이유를 명료하게 정리하자면 아래와 같다.

* 기존 소스코드의 스타일링은 일관성이 없었음
  * styled-component의 Theme를 활용하면 서비스 전반에 사용될 스타일링을 일관성있고 효율적으로 가능
  * JavaScript로 스타일을 정의할 수 있으므로 동적이고 유연하게 스타일을 적용할 수 있음
  * 다크모드를 적용하기에 매우 유용
* BEM 방식의 장황한 클래스 작명에서 벋어날 수 있음
  * 상기 classnames와 BEM 방식의 클래스 작명이 합쳐지면 가독성이 끔찍하게 저하되는 문제가 있어왔음



## 2. Theme

* TypeScript의 interface를 정의하고 Theme를 사용



### theme.d.ts

* styled-components에 정의되어 있는 빈 interface인 DefaultTheme을 프로젝트 Theme에 맞게  정의

```React
import 'styled-components';

declare module 'styled-components' {
  export interface DefaultTheme {
    fontSizes: {
      title: string
    };
    colors: {
      bg: string;
    };
  }
}
```



### theme.ts

* enum을 활용하여 Theme에 사용되는 고정된 값들을 정의
* enum이란?
  * 열거형으로 이름이 있는 상수들의 집합을 정의할 수 있음
  * 기본적으로는 숫자 열거형
  * 각 요소에 문자열을 할당하면, 문자열 열거형으로 정의 됨
  * **vs. object : 객체의 경우 참조값이므로 const로 선언하여도 해당 프로퍼티들의 변경이 가능하지만 enum은 읽기 전용의 상수 취급되어 재할당이 방지 된다!**

```React
import { DefaultTheme } from 'styled-components';

// 고정될 값들을 문자열 열거형으로 정의
enum FontSizes {
 	title = 20px,
}

enum Colors {
  white = '#ffffff',
  gray = '#222222'
}

// 다크모드, 라이트모드에 따라 다른 값들이 들어가므로 테마에 맞게 지정
export const lightTheme: DefaultTheme = {
  fontStyles: { ...FontSizes },
  colors: {
		bg: Colors.white,
    text: Colors.gray,
  },
};

export const darkTheme: DefaultTheme = {
  fontStyles: { ...FontSizes },
  colors: {
		bg: Colors.gray,
    text: Colors.white,
  },
};
```



### App.tsx

* 정의한 테마를 styled-component에서 지원하는 ThemeProvider로 최상위 컴포넌트에서 하위 컴포넌트들로 주입
  * 주입한 theme의 값들은 ThemeProvider 하위의 컴포넌트 들에서 props로 접근할 수 있음

```React
...
import { ThemeProvider } from 'styled-components';
import { lightTheme } from './themes';

function App() {
  return (
    ...
          <ThemeProvider theme={lightTheme}>
            // components
          </ThemeProvider>
...
  );
}

export default App;
```



## 3. GlobalStyle

- styled-components로 전역 스타일 정의를 할 수 있음
- createGlobalStyle: 전역 스타일을 적용할 수 있는 컴포넌트 API

```React
import { createGlobalStyle } from 'styled-components';

const GlobalStlye = createGlobalStyle`
	  // css reset 및 전역 스타일링
`;

export default GlobalStlye;

-------------------------------------------
  // export한 GlobalStyle을 아래와 같이 상위에서 적용토록 선언해줌
 ...
import GlobalStlye from './GlobalStyle';

function App() {
  return (
    ...
          <ThemeProvider theme={lightTheme}>
						<GlobalStlye />
            // components
          </ThemeProvider>
...
  );
}

export default App;
```



## 4. 느낀점

현재 본격적으로 해당 프로젝트의 프론트엔드 작업 중인데, styled-component는 대단히 편하고 유용한 라이브러리인 것 같다. 상기한 기능 말고도 React Component의 props와 연계하여 동적으로 스타일링을 하는 방식으로 컴포넌트를 확장시킬 수도 있다.



## 5. 참고 문헌

* [styled-components](https://styled-components.com/)

* [JavaScript With Syntax For Types.](https://www.typescriptlang.org/ko/)

