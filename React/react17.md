# 코드 분할

* 번들링
  * Webpack과 같은 툴을 사용하여 여러 파일을 하나로 번들링
  * 번들링된 파일을 한 번에 로드하여 앱을 실행




## 1. 코드 분할

* 규모가 큰 앱을 번들링하면, 로드시간이 길어 짐
  * 이를 방지하여, 코드를 나누기
* 런타임에 여러 번들을 동적으로 불러옴
* 지연 로딩을하여, 성능 향상을 시킬 수 있음



## 2. Suspense & React.lazy

* Suspense 컴포넌트 하위에서 사용 가능
  * 컴포넌트가 로드되길 기다리는 동안 예비 컨텐츠를 보여줄 수 있음(ex. 로딩 화면)
  * fallback : 컴포넌트가 로드될 때까지 기다리는 동안 보여줄 React 엘리먼트를 넘길 props
  * 하나의 Suspense 컴포넌트로 여러 lazy 컴포넌트를 감쌀 수 있음
* React.lazy는 동적 import를 호출하는 함수를 인자로 가짐
  * 이 함수는 React 컴포넌트를 default export로 가진 모듈 객체가 이행되는 Promise를 반환해야 함
  * default exports만 지원

```React
import React, { Suspense } from 'react';

const InnerComponent = React.lazy(() => import ('./innerComponent'));

function OuterComponent() {
  return (
  	<div>
      <!-- 로딩중인 것을 표시 -->
    	<Suspense fallback={<div>로딩중</div>}
        <OuterComponent />
			</Suspense>
    </div>
  )
}
```



### Error boundaries

* 네트워크 장애로 인해 모듈 로드에 실패할 경우 에러를 발생시킬 수 있음
* Error Boundary 컴포넌트를만들고 lazy 컴포넌트를 감싸기
* Error Boundary는 오직 클래스 컴포넌트만 가능

```React
import React, { Suspense, lazy } from 'react';
import ErrorBoundary from './ErrorBoundary';

const InnerComponent = lazy(() => import ('./innerComponent'));

function OuterComponent() {
  return (
  	<div>
      <ErrorBoundary>
      	<!-- 로딩중인 것을 표시 -->
        <Suspense fallback={<div>로딩중</div>}
          <OuterComponent />
        </Suspense>
      </ErrorBoundary>
    </div>
  )
}
```



## 3. Route-based code splitting

* 사용자 경험을 해치지 않으면서 번들을 나누기 좋은 것은 라우트
* 웹 페이지를 불러오는 시간은 어느 정도 발생
* 사용자가 페이지를 렌더링하는 동안에는 다른 요소와 상호작용 하지 않음

```React
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import ErrorBoundary from './ErrorBoundary';

const Main = lazy(() => import ('./routes/Main'));

function OuterComponent() {
  return (
  	<Router>
      <ErrorBoundary>
      	<!-- 로딩중인 것을 표시 -->
        <Suspense fallback={<div>로딩중</div>}
          <Route path="/" element={<Main />} />
        </Suspense>
      </ErrorBoundary>
    </Router>
  )
}
```



# Reference

[React 공식 문서](https://ko.reactjs.org/)

