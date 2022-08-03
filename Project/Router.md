

# Router

## 서론

이전에는 기본적인 구조와 디자인 패턴을 정하였다. 그 다음으로는 소스코드 전반에 걸쳐 사용될 Router 구성 전략을 세우고 실제로 어떻게 적용할 것인지 예시를 들어볼 것이다.



## 1. Router 구성 전략

* 사용할 패키지는 react-router-dom 패키지를 사용

  v6이 나왔다. Major 버전 업데이트라서 여러가지 변화한 부분들이 많은데, 추후 개발을 위해서라도 처음부터 v6를 쓰는 것이 유지, 보수 측면에서 좋을 것 같다고 생각하였다. 배우는 데 약간의 시간이 걸리더라도 그 비용이 그리 크지 않았고 당장의 도입을 위해 v5를 도입하면 기술부채가 생겨버리는 것이기 때문이었다. 또 Switch가 Routes로 바뀌고 exact가 없어지는 등 더 직관적이고 사용하기 편리해졌다는 생각이 들었다.

* 로딩시간 단축을 위해, React.lazy와 Dynamic Import를 사용

  CRA는 진입시에 로딩이 길다는 단점이 있는데 이와 같은 Code Spliting을 통해 쪼개놓으면 로딩 시간을 단축시킬 수 있는 이점이 있다.

* Route path는 path를 등록하고 접근할 수 있도록 별도의 객체를 선언

  TypeScript의 as const를 사용하여 변경을 방지하고 접근만 가능하도록 한다.

* 더하여

  React에서 제공하는 기능인 ErrorBoundary, Suspense를 필요한 Route에 적용하여 선언적인 에러처리와 로딩처리를 할 것이다.



## 2. Route Path

* 각 페이지의 URL를 등록하고 접근할 수 있는 객체

* as const를 사용하여 접근만 가능하도록 하기

* key는 컴포넌트 명, value는 그 컴포넌트에 접근하기 위한 url을 명시

* depth는 1 depth로 얕게

  기존 메인 app의 방식은 Route Path에 공통 경로를 묶는 방식으로 정의하였는데 depth가 너무 깊어져 가독성이 떨어졌었음



### 예시

```TypeScript
const path = {
  home: '/',
  login: '/login',
  ...
} as const;
```





## 3. Code Spliting

* 코드 분할을 통해 로딩 시간 단축을 꾀함
* React.lazy는 동적 import를 사용하여 컴포넌트 렌더링 가능



### 예시

```React
import React, { lazy } from 'react';
import { Routes, Route } from 'react-router-dom';
import path from './path';

const Home = lazy(() => import('./pages/home'));
const Login = lazy(() => import('./pages/Login'));

function App() {
  return (
        <Routes>
          <Route path={path.home} element={<Home />} />
          <Route path={path.login} element={<Login />} />
      		<!-- *은 정의한 경로 외 다른 경로 접근시 -->
          <Route path="*" element={<NotFound />} />
        </Routes>
  );
}

export default App;
```



## 4. 느낀점

위와 같이 모든 세팅을 했지만 어째서인지 라우팅이 되지 않고 404 error가 발생하였다. react-router-dom의 docs을 보며 몇가지 시도를 해보았지만 해결이 되지 않았었다. 많은 시행착오(삽질...) 끝에 구글에서 해당 이슈의 원인과 해결법을 찾을 수 있었다. 바로 webpack의 devserver 설정 문제였다.
기존의 SSR의 경우 사용자가 특정 url에 접근하면 그것에 해당하는 페이지를 응답한다.
반면, React같은 SPA은 CSR로 이루어진다. 하나의 HTML 파일만 있으니 기존의 방식대로 라우팅 처리를 하면 해당 url의 HTML을 찾을 수 없으니 404 error가 발생하는 것이다. 그러므로 아래와 같이 웹팩 세팅을 해주면 된다. 그러면 webpack의 devserver가 url에 정상적으로 접근토록 처리해준다.

```JavaScript
devServer: {
   historyApiFallback: true,
		...
},
```



## 5. 느낀점

Router를 구성하는 것 자체는 어렵지 않았다.
하지만, 4번의 이슈에서는 적잖이 당황했다. Router를 위한 모든 세팅을 다 했음에도, docs를 보았음에도 불구하고 해결이 되지 않았기 때문이다.
상기와 같이, 원인은 정말 흥미롭게도 CSR에 있었다. 그리고 해결은 웹팩으로 해낼 수 있었다. 보통 프로젝트를 할때는 간단하게 CRA로 세팅을 했었는데 이때는 마주치지 못했던 이슈였다. 이번에는 다행히(?)도 웹팩으로 세팅하게 되었고 그 결과 이런 이슈를 겪을 수 있었다. SSR과 CSR의 차이점은 알고 있었으나 이론적인 면에서만 그쳤었는데 이렇게 실무에서 마주치니 좀 더 와닿게 이해할 수 있게된 기회였던 것 같다.




## 5. 참고 문헌

* [React-router URLs don't work when refreshing or writing manually](https://stackoverflow.com/questions/27928372/react-router-urls-dont-work-when-refreshing-or-writing-manually)
* [react-router](https://v5.reactrouter.com/web/guides/quick-start)

