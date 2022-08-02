

# Suspense & ErrorBoundary

## 서론

기존의 리액트 소스코드를 다루면서, 로딩처리와 에러처리는 많이 하게 되는 일들이다.
로딩 처리는 API를 호출하고 그 응답을 기다리는 동안 사용자에게 로딩 화면을 보여주는 처리이다. UX 측면에서 있어야하는 것이고 동시에 불러오지 않은 데이터에 접근함으로 발생하는 에러또한 막을 수 있다.
에러처리는 async를 사용한다면 보통 try, catch문을 사용하고 Promise Chaining을 사용한다면 catch 메서드를 사용하여 다루게 된다. 분명 에러를 방지하여 런타임 자체가 죽어버리는 문제는 막을 수 있지만 문법 특성상 반복적으로 사용할 수밖에 없다. 특히 프로젝트에서 API 호출이 많아질수록 에러처리에 대한 보일러플레이트가 그에 비례하여 늘어난다.
React에서는 이 두 처리를 선언적으로 할 수 있는 유용한 컴포넌트들을 제공하는데 바로 Suspense와 ErrorBoundary이다.



## 1. Suspense
* 로딩 처리를 선언적으로 할 수 있음
* 아직 React에서 지원하는 Suspense만으로는 비동기 로딩을 구현할 수는 없음
* react-query를 사용하면, 비동기 로딩도 구현할 수 있음
  * react-query의 suspense 옵션으로 Suspense를 비동기 로딩에 사용 가능
  * 하위 컴포넌트에서 API 응답을 기다리는 중일 때(Promise Pending), 상위에서 감싸는 Suspense가 이를 감지하여 fallback 프로퍼티에 명시된 컴포넌트를 보여줌



### 로딩 처리의 기존 방식 vs. Suspense

기존의 방식은 로딩 처리를 위해 필요한 코드들이 너무 많음

```React
import React, { useState } from 'react';

function Page() {
	const [loading, setLoading] = useState(true);

	const fetchData = async () => {
			// ... 비동기 실행
			const response = await api.fetchData();
			setLoading(false);
	}

	if (loading) {
		return <h1> 로딩중 ... </h1>
	};

	return (
		<div>
			...컨텐츠
		</div>
	);
}

export default Page;
```

아래와 같이 Suspense로 선언적인 로딩 처리 가능

```React
...

function App() {
  return (
      <Suspense fallback={<Loading />}>
        <Routes>
          <!-- 아래의 컴포넌트들에서 API 요청 후 대기중일 때(Promise Pending) fallback에 명시된 컴포넌트를 보여줌 -->
          <Route path="/" element={<Home />} />
          <Route path="/login" element={<Login />} />
          <Route path="*" element={<NotFound />} />
        </Routes>
      </Suspense>
  );
}

export default App;
```





## 2. ErrorBoundary

>  페이스북 메신저는 사이드 바, 정보 패널, 대화 기록과 메시지 입력을 각각 별도의 에러 경계로 감싸두었습니다. 이 UI 영역 중 하나의 컴포넌트에서 충돌이 발생하면 나머지 컴포넌트는 대화형으로 유지됩니다.

* 오류를 잡아내는 컴포넌트
* 단, 이벤트 핸들러, 비동기적 코드, 서버 사이드 렌더링, 에러바운더리 자체 에러의 에러는 잡지 못함
  * **react-query와 함께 사용하면, 비동기 처리에서도 ErrorBoundary를 사용 가능**
  * 이벤트 핸들러의 경우 try, catch를 사용하면 됨
* 보일러 플레이트를 방지하고 선언적으로 에러를 잡고 로깅에도 활용할 수 있음
* 특정 Error Exception을 감지하여 로직을 정리 할 수도 있음
* ErrorBoundary는 내부적으로 에러를 잡아내는 Life Cycle Method를 사용하는데, Hook에서는 아직 지원하지 않아 Class Component로 정의해야 함



### 예시

```React
import React, { Component, ErrorInfo, ReactNode } from 'react';

interface Props {
  children: ReactNode;
}

interface State {
  hasError: boolean;
}

class GlobalErrorBoundary extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: Error) {
		// Error을 캐치하여 state.hasError 변경
    return { hasError: true };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
		// Error을 캐치하여 로깅
    console.error(error, errorInfo);
  }

  render() {
    const { hasError } = this.state;
    const { children } = this.props;
		// hasError가 true이면, 에러 화면을 보여줌
    if (hasError) {
      return <h1>Error</h1>;
    }

    return children;
  }
}

export default GlobalErrorBoundary;
```





## 3. 느낀점

React의 방향성은 선언적인 프로그래밍이다. Suspense와 ErrorBoundary는 그에따라 등장했다고 볼 수 있다. 
협업에 있어서, 선언형 프로그래밍은 대단히 유용하다고 생각한다. 현업에서 다루었던 코드는 주로 명령형 코드로 되어있었는데(특히 레거시 코드의 Vanila JavaScript, Jquery) 유지, 보수하기 대단히 힘들었다. 그에 반해, 선언형 코드로 되어있는 강의 코드, Code Pen의 예시들을 보면 로직을 파악하기 쉬웠다.그래서, 이번 화상 프로젝트에서는 선언형 프로그래밍을 주된 방법론으로 채택하였다. 여러 팀원들과의 협업에서 좋은 효과를 낼 수 있을 것으로 기대되기 때문이다. 그런 맥락에서 Suspense와 ErrorBoundary를 도입하게 된 것이다
다만, 아직 단점이 있는데 Suspense와 ErrorBoundary가 공통적으로 비동기에 대해서 지원이 미흡하다는 점이다. 로딩과 에러 자체는 주로 Data Fetching에서 일어날 것들이라 조금 난처하였는데, 다행히도 react-query에서는 이 둘의 비동기 처리를 보조해줄 수 있다. 그래서 Data Fetching에서는 react-query를 도입할 예정이다.



## 5. 참고 문헌

* [Suspense]([초간단 비동기 렌더링 React Suspense](https://www.youtube.com/watch?v=8q7OQSPLF4k))
* [ErrorBoundray]([Error Boundaries | React TypeScript Cheatsheets](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/error_boundaries/))
* [React ErrorBoundary docs](https://ko.reactjs.org/docs/error-boundaries.html)

