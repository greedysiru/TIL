# 에러 경계

## 1. 에러 경계란

* 자바스크립트 에러가 전체 애플리케이션을 중단시켜서는 안 됨
  * 이를 해결하기 위해 에러 경게가 도입
* 하위 컴포넌트 트리의 어디에서든 자바스크립트 에러를 기록
* 깨진 컴포넌트 트리 대신 폴백 UI를 보여주는 컴포넌트
* 에러 경계가 에러 메시지를 렌더링하는 것에 실패하면 그 위의 가까운 에러 경계로 전파됨
* 선언적인 표현
* vs. try/catch
  * 명령형 코드에서 동작
  * 이벤트 핸들러에서 사용할 것



## 2. 에러 경계가 포착하지 못하는 것

* 이벤트 핸들러
* 비동기적 코드
* 서버사이드 렌더링
* 에러 경계 자체의 에러



## 3. 사용법

### 에러 경계 정의

* 에러 경계는 클래스에서 정의해야 함
* 생명주기 메서드인 아래 2 가지 메서드를 사용
  * static getDerivedStateFromError
  * componentDidCatch

```React
class ErrorBoundary extends React.component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }
  
  static getErivedStateFromError(error) {
    // 다음 렌더링에서 폴백 UI가 보이도록 상태 업데이트
    return { hasError: true }
  }
  
  componentDidCatch(error, errorInfo) {
    // 에러 리포팅을 할 수 있음
    errorTracker(error, errorInfo);
  }
  
  render() {
    if (this.state.hasError) {
      // 콜백 UI
			return <h1>에러!</h1>
    }
    
    // 에러가 발생하지 않으면 정상적인 렌더링
    return this.props.children;
  }
}
```



### 에러 경계 사용

```React
// 정의한 에러 경계를 감싸기
<ErrorBoundary>
	<Component />
</ErrorBoundary>
```



## 4. 에러 경계 위치

* 최상위 경로에서 유저에게 문제 피드백
* 에러 경계를 감싸서 애플리케이션의 부분간에 충돌 방지



## 5. 리액트의 에러 동작

* React 16부터 에러 경계에서 포착되지 않은 에러로 인해 전체 React 컴포넌트 트리의 마운트가 해제
  * 즉, 아무것도 렌더링이 안 됨
* 에러 경계를 활용하여 문제 발생시 더 나은 사용자 경험 제공
  * ex) 페이스북 메신저는 사이드 바, 정보 패널, 대화 기록 등을 에러 경계로 감싸두었음



## 6. 컴포넌트 스택 추적

* React 16 이후 렌더링 동안 발생한 모든 에러를 콘솔에 출력
  * 컴포넌트의 어느 트리에서 에러가 발생했는 지 알 수 있음
* 프로덕션 환경에서는 비활성화 해야 함

# Reference

[React 공식 문서](https://ko.reactjs.org/)

