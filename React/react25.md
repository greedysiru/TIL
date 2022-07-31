# Effect Hook 사용하기(2)



## 1. Clean-up Effects vs. non-clean-up Effects

* side effect를 실행 하고 나서 후처리가 필요한 경우가 있음
* Clean-up이 필요한 경우
  * 외부 데이터를 구독하는 경우
  * addEventListener를 지정한 경우
  * why? 메모리 누수 방지를 위해
* Clean-up이 필요하지 않은 경우
  * API 호출
  * DOM 수동 조작
  * 로깅
* **effect에서 함수를 반환하는 이유**
  * effect를 위한 추가적인 정리 메커니즘
  * effect의 추가와 제거 로직을 가까이 묶을 수 있음
* **React가 effect를 정리(Clean-up)하는 시점**
  * 컴포넌트가 마운트 해제되는 때에 정리(Clean-up) 실행



### Clean-up Effects 예시

* event listener를 Clean-up
* Class Component의 Life Cylce Methods로 구현하는 경우
  * componentDidmount에서는 event listener 등록을
  * componentWillUnmount에서는 event listener Clean-up을 해야 함

```React
useEffect(() => {
  ...
  element.addEventListener('click', handleClick);
  
  return () => {
    element.removeEventListener('click', handleClick);
  }
});
```



## 2. Multiple Effect

* 여러 useEffect를 사용하여, 관심사를 구분하는 방법
  * 모든 effect를 지정된 순서에 맞추어 적용
* 기존 Class Component의 Life Cycle Methods의 문제는 시점 기준으로 로직이 묶이기 때문에 Component에 필요한 side effect가 많아지는 경우 관련 없는 로직들이 뭉쳐질 수 있음
  * 반면, 관련 있는 로직은 실행 시점에 따라 파편화될 수 있음



## 3. Dependancy Array

* 특정 state를 Dependacy Array에 넘겨 state가 변경되었을 때만 effect를 재실행
* 컴포넌트가 리렌더링 되었을 때, 전달 받은 state를 이전 렌더링 시전의 state와 비교하여 다른 경우, effect를 재실행
* Dependacny Array를 사용한다면, effect에 의해 사용되는 값들을 모두 포함할 것
  * 그렇지 않는다면, 이전의 렌더링 값을 참고하게 됨
* 빈 배열을 넘기면, 첫 렌더링(마운트) 시에만 한 번만 실행 됨

```React
useEffect(() => {
  const fetchUserInfo = async () => {
    ...
  }
  // userId가 변경되었을 때만 effect를 재실행
}, [userId]);
```



## 4. 정리 및 느낀점

왜 React 팀은 구현되어 있던 Class Components의 Life Cylce Methods가 있음에도 불구하고 Hook을 구현했을까? 답은 바로 **관심사의 분리**이다.
어찌보면,  Life Cylce Methods들은 명시적으로 시점을 칭하고 있기 때문에 받아들이기 더 쉬울수는 있다. 하지만, 컴포넌트가 비대해지고 많은 side effect를 사용해야하는 경우면 로직이 복잡해질수밖에 없다. 왜냐하면 시점에따라 side effect를 넣어야하니 관련 없는 로직이 섞이고 관련 있는 로직은 파편화될 수밖에 없기 때문이다. 이와 비교하여 useEffect는 여러개를 호출하여 관련 로직들끼리 정리해둘 수 있다. 즉 **관심사를 분리**할 수 있다.

나는 현재 근무를 하며 React.js와 Vue.js를 다루고 있다. Vue.js의 Instance Life Cycle Hook은 React.js의 Life Cylce Methods와 동일한 역할을 한다고 볼 수 있다. Vue Instance의 Life Cycle 시점에 따라 로직을 지정할 수 있기 때문이다.
이러한 대목에서, Vue.js는 단순한 페이지 및 컴포넌트를 구현하는 것에는 생산성이 좋고 직관적이라고 할 수 있으나 복잡한 로직을 구현해야하는 경우라면 Life Cylce Methods처럼 서로 다른 로직이 섞이고 관련 로직이 파편화될 수 있다.

React.js가 현재 프론트엔드 진영에서 압도적인 사랑을 받는 이유 중 하나는 위에서 말했듯, 선언적이고 관심사의 분리를 철저히 할 수 있는 useEffect 같은 Hook의 존재라고 할 수 있을 것 같다. 웹 애플리케이션이 점점 고도화가 되며 그 복잡성이 높아지고 있는데 이를 해결해줄 수 있는 여지를 주기 때문이다.





# Reference

[React 공식 문서](https://ko.reactjs.org/)

