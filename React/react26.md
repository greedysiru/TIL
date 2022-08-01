# Hook 규칙, Custom Hook



## 1. Hook 규칙

* 최상위에서만 Hook을 호출
  * 반복문, 조건문, 중첩된 함수에서 Hook 호출하지 말 것
  * 조건문을 Hook내부에 사용하는 것은 가능(useEffect)
  * 이 규칙을 따라야 동일한 순서로 Hook 호출되는 것이 보장
* React 함수 내에서만 Hook을 호출
  * JavaScript 내에서 호출하지 말 것
* 규칙을 지켜야하는 이유
  * 모든 상태 관련 로직을 소스코드에서 명확하게 보이도록 할 수 있음



## 2. Custom Hook

* 컴포넌트 로직을 함수로 뽑아 재사용
* **공통의 로직을 뽑아내 새로운 함수를 만드는 것으로 작동 방식과 순서에는 변화가 없음**
* 관습적으로 use prefix를 붙일 것
* **같은 Hook을 사용하는 컴포넌트들은 state를 공유하지 않음**
  * 서로 독립된 state를 받음
  * 기존의 Hook과 동일하게 각각 독립적으로 동작



### 예시

```React
import { useState, useCallback } from 'react';

const useInput = (initialValule: string) => {
  const [value, setValue] = useState(initialValule);

  const onChange = useCallback((event: { target: HTMLInputElement }) => {
    setValue(event.target.value);
  }, []);

  return { value, onChange };
};

export default useInput;
```



## 3. 정리 및 느낀점

Hook 규칙의 경우, React를 배운지 얼마 안 되었을 때 매번 ESLint에게 지적당했던 것들 중 하나이다. if문으로 특정 조건일 때만 side effect를 실행하고 싶었는데 왜 이런 규칙이 있는 지 이해할 수 없었다. 하지만 이 문서에서, 들은 예시중 각 렌더링 시점마다의 if문을 통과할 수도 통과하지 못할 수도 있다. 그렇게 되면 Hook이 정의된 순서대로 진행하려다가 순서가 밀리면서 버그가 발생할 수도 있다.
Custom Hook은 React 함수형 컴포넌트의 강력한 기능 중 하나라고 생각한다. 중복 로직을 Hook으로 묶어서 재사용성을 높이고 선언적인 프로그래밍을 할 수 있기 때문이다. 아직은 좋은 코드를 작성하지 못해서 잘 활용하지는 못하고 있지만 새로 진행하는 프로젝트에서 여러 Hook을 도입하려하는 등 많은 시도는 하고 있다.

# Reference

[React 공식 문서](https://ko.reactjs.org/)

