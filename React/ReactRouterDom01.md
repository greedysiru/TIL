# React Router Dom(1)

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. Router States

* React Router Dom에서 제공하는 Link 컴포넌트를 활용하여 현재 화면의 데이터를 다른 화면으로 보낼 수 있음
* 이미 가지고 있는 데이터를 활용하여 다음 페이지의 화면 렌더링
  * 좋은 UX 제공
* useLocation: Router State에 접근할 수 있는 Hook



### 예시

```React
import { Link } from 'react-router-dom';
...

function PreviousPage() {
  return (
    <>
    	<h1>이전 페이지</h1>
    	<Link to={{
              pathname: `/nextPage`,
              state: { text: '이전 페이지로부터 이동했습니다.' },
            }}>
              다음 페이지 가기
      </Link>
    </>
  );
};
```

```React
import { useLocation } from "react-router-dom";

function NextPage() {
  const {state} = useLocation();
  return (
    <>
    	<h1>다음페이지 페이지</h1>
			<span>이 페이지는 ${state.text}</span>
    </>
  );
};
```



## 2. Nested Router

* route안에 있는 또 다른 route
* 웹사이트 탭 기능을 구현
  * 스크린 안에 섹션이 나뉘어졌을 때
* state로 관리하는 대신에 URL에서 관리
  * URL로 관리하는 것이 사용자가 바로 접속할 수 있어 더 유용
* **Nested Route로 이동을 하여도 감싸고 있는 route는 리렌더링되지 않음**

```React
<Switch>
  <Route path={`/myPage/email`}>
    <Chart />
  </Route>
  <Route path={`/myPage/password`}>
    <Price />
  </Route>
</Switch>
```



## 3. useRouteMatch

* 현재 URL이 명시한 URL과 같은 곳인지를 알려주는 Hook
* 명시한 URL에 위치하면 해당 라우트에 대한 정보 객체를 return
  * 아니라면 null

```react
  const emailMatch = useRouteMatch("/myPage/email");
  const passwordMatch = useRouteMatch("/myPage/password");
```



# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

