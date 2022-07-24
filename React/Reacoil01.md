# Recoil(1)

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. Recoil 이란?

* React JS에서 사용할 수 있는 state management library
* 여러 컴포넌트에서 전역적인 상태값에 접근 또는 변경할 수 있음
  * ex) 다크 모드, 로그인 상태(인가)
* 전역 상태관리 없이 전역적인 상태값을 사용하려면 props Drilling이 일어날 수 있음
  * props Drilling: 하위 컴포넌트로 상태를 넘기기 위해 props를 그 컴포넌트까지 여러번 넘겨야 하는 것
  * 규모가 큰 앱일수록 하위 컴포넌트가 많아지고 이 컴포넌트들에 상태를 props 전달을 위한 코드를 반복적으로 써야 함
  * 문제의 원인 파악에도 어려움


## 2. atom

* 상태의 일부를 나타냄
* 어떤 컴포넌트에서나 읽고 쓸 수 있음
  * 해당 atom을 읽는 컴포넌트는 atom을 구독
  * 어떤 변화가 있으면, 구독하는 컴포넌트는 재 렌더링
* 컴포넌트들과는 독립적



```JavaScript
import { atom } from "recoil";

// 로그인 상태를 전역적으로 관리하기 위한 atom
export const isLoggedInAtom = atom({
  // 해당 atom에 대한 유일한 ID
  key: "isLoggedIn",
  // 기본값은 false(비로그인 상태)
  default: false,
});

```



## 3. useRecoilValue

* 등록한 atom에 접근하는 hook
  * atom의 상태를 return

```React
import { useRecoilValue } from "recoil";
import { isLoggedInAtom } from "./atoms";

function MainPage() {
  // 현재 isLoggedInAtom의 상태에 접근
  const isLoggedIn = useRecoilValue(isLoggedInAtom);
  return (
    <>
          <title>{isLoggedIn? '로그인되었습니다.' : '로그인이 필요합니다.'</title>
    </>
  );
}

export default MainPage;

```



## 4. useSetRecoilState

* 등록한 atom의 상태를 설정하는 Hook
  * Setter Function을 return

```react
import { useSetRecoilState } from "recoil";
import { isDarkAtom } from "../atoms";


function LoginPage() {
  // Setter Function: atom을 설정(set)하는 Function
  const setIsLoggedInAtom = useSetRecoilState(isLoggedInAtom);
  // 이전 isLoggedInAtom 상태의 반대를 return하는 이벤트 핸들러
  const toggleDarkAtom = () => setIsLoggedInAtom((prev) => !prev);
	  <>
      ...
      <button onClick={toggleDarkAtom}>로그인하기</button>
    </>
  );
}

export default LoginPage;
```



# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

[Recoil Docs](https://recoiljs.org/ko/)

