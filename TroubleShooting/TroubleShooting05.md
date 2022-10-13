# useCallback과 클로져 그리고 의존성 배열

   

   ## 1. useCallback이란?

useCallback은 함수를 전달받아 메모이제이션한다. 불필요한 렌더링을 방지하여 성능 최적화를 위해 사용되는 React Hook이다.

이 Hook 또한 useEffect와 마찬가지로 두번째 인자로 의존성 배열을 전달할 수 있다. 의존성 배열에 전달된 변수가 변경이 일어나면 콜백함수는 재차 메모이제이션된다.

```JavaScript
const exampleCallback = useCallback(() => exampleFunction(a), [a]);
```



   

   ## 2. 이슈 발생

최근에 지인이 진행하던 프로젝트에 합류하게 되었다.
react-dnd를 활용하여 생성된 리스트를 drag & drop으로 옮길 수 있는 기능을 구현했는데, UI 자체는 이동이 되나 그 데이터가 제대로 적용이 되지 않는 이슈가 발생했다.



## 3. 원인 파악

리스트의 데이터 하나 하나는 recoil atom으로 구성되어있었고 그 각각의 요소들을 recoil factory id로 관리하고 있었다. 그런데 drag & drop을 하여 요소의 순서를 바꿨을 때, 이 id들이 순서에 맞게 최신화가 되지 않았다. 이 문제를 파악하기 위해서 우선 drag & drop 로직 함수를 찾아내었다.

```JavaScript
const onMove = useCallback(
    (dragIndex: number, hoverIndex: number) => {
      const idList = questionItemIdList[dragIndex];
     // react-dnd 로직
      ...
    []
  );
```

위와 같이 해당 함수는 useCallback으로 메모이제이션되어 있는 형태였다. 여기에서, idList라는 변수에 questionItemIdList라는 recoil state를 가져오는데, 이것이 문제로 의심되었다. useCallback은 콜백을 메모이제이션하는데, 함수 내부에서 외부의 값을 참조하면 이것이 바로 클로저가 되기때문이다. 더군다나 의존성 배열도 아무것도 들어있지 않았다.

클로저로 인해서 drag&drop이 일어나 리스트의 순서가 변경되어도 questionItemIdList는 메모이제이션된 시점의 값을 가지고 있으므로 최신화가 되지 않은 잘못된 상태로 ui가 렌더될 것이다.

   ##     

   ## 3. 해결 방법

다행히, 아주 간단하게 해결할 수 있었다. 의존성 배열에 questionItemIdList를 넣어주니 제대로 동작하였다.

```JavaScript
const onMove = useCallback(
    (dragIndex: number, hoverIndex: number) => {
      const idList = questionItemIdList[dragIndex];
     // react-dnd 로직
      ...
    [questionItemIdList]
  );
```

   

   ## 4. 고찰

클래스 컴포넌트만이 존재했던 시절은 공통로직을 컴포넌트에서 사용하기위해서 HOC를 활용해왔다. 하지만, depth가 깊어지면 추적이 어렵게 된다. (마치 비동기 처리에서의 콜백헬과 같은 맥락으로 볼 수 있다.)

반면,  React Hook은 계층의 변화 없이 상태 관련 로직을 재사용할 수 있도록한다. react 컴포넌트에서 독립적으로 동작하는 Hook을 사용하여 추적이 용이하고 안정적으로 로직을 구현해낼 수 있다.

도구를 사용할 때는 그 사용법을 정확하게 알아야한다. 이 글의 useCallback 클로저 이슈처럼 말이다. useEffect, useCallback에서 의존성 배열의 의미를 정확하게 이해하고 용도에 맞게 로직을 구현해 낼 수 있어야 한다.

사실, 리액트 공식 문서에서도 소개되어 있는데 eslint에서 exhaustive-deps 규칙을 사용하면, Hook에서 참조하는 변수를 의존성 배열에 넣어줄 것을 강제하거나 주의를 줄 수 있다. 하지만, 나는 이 옵션을 키는 것은 반대다. 왜냐하면, 의도치 않은 동작을 일으킬 수 있기 때문이다.

```JavaScript
useEffect(() => {
  const fetchData = async (params) => {
    // API 호출
    const {data} = await API(params);
    parsingFunction(data);
  }
  fetchData();
}, [params, parsingFunction])
```

예를 들어, 위와 같은 API 호출과 같은 비동기 함수 fetchData를 사용하는 useEffect가 있다고 하자. 그리고 해당 함수는 params를 받아 API 호출을 하고 응답 받은 값을 parsingFunction에 전달한다. exhaustive-deps 규칙의 경우 이 params, parsingFunction를 의존성 배열에 넣을 것을 요한다. 여기서, params가 고정된 값이라면 큰 영향은 없을 것이다. 하지만, useState와 같이 특정 상황에 따라 값이 변한다면, 의도치 않게 useEffect가 실행될 수도 있다. 또 parsingFunction와 같은 함수가 모듈 로직이 아니라 해당 컴포넌트 내부에서 적용된 경우 컴포넌트가 재렌더 되면 함수 또한 재할당이 일어나므로 useEffect가 실행이된다. 이런 이유로, useEffect안에서 사용되는 변수, 함수들을 모두 의존성 배열에 넣으면 개발자가 의도치 않은 버그, 무한렌더링이 발생할 수 있다. 때문에, 나는 개발자가 판단하여 의존성 배열을 넣는것이 맞다고 생각한다.

   

   ## Reference

   * [React useCallback Hook Api](https://ko.reactjs.org/docs/hooks-reference.html#usecallback)
   * [React Hook Motivation](https://ko.reactjs.org/docs/hooks-intro.html#motivation)