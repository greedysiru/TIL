# 타입 단언과 타입 가드 - 타입 단언은 지양하자

## 1. 타입 단언이란?

타입 단언이란, 타입을 구체적으로 명시하는 방법이다. 때로는 타입 추론보다 개발자가 타입에 대해서 자명하게 알 때가 있다. 대표적인 예시로는 아래처럼 react 프로젝트의 index.tsx에서의 코드를 들 수 있다.

```
import React from 'react';
import { createRoot } from 'react-dom/client';

const root = document.getElementById('root') as HTMLElement;

createRoot(root).render(<App />);
```

위처럼 타입단언을 해야하는 이유는 아래와 같다.

1. getElementById DOM API는 해당하는 id를 가지는 **element 또는 null을 반환**
2. createRoot react API는 **Element 또는 DocumentFragment** 받아야 함
3. getElementById의해 root에는 null이 할당될 수 있으므로 creatRoot에서 ts(2345) 에러가 발생(적절하지 않은 타입을 넘겼으므로)
4. **react 프로젝트에서는 root 아이디를 가진 element가 반드시 존재함이 자명하므로 타입 단언 처리**

##  

## 2. 타입 단언 트러블

현업에서, 타입 단언을 남발하다가 트러블이 발생한 적이 있다. **API 응답을 담는 변수들에 타입 단언을 붙인 경우였다.**

```
// 보통은 useEffect, useState를 사용하여 API 비동기 처리와 상태를 관리하지만, 해당 코드에서는 다소 생략함
// API 응답에 타입 단언을 사용한 것에 주목
const response = fetchAPI('/users') as User;

return <h1>response.name</h1>
```

타입단언에 대해, TypeScript 공식 Docs에서는 이렇게 말한다.

> 기억하세요: 타입 단언은 컴파일 시간에 제거되므로, 타입 단언에 관련된 검사는 런타임 중에 이루어지지 않습니다. 타입 단언이 틀렸더라도 예외가 발생하거나 null이 생성되지 않을 것입니다.

즉, 애플리케이션이 동작하는 런타임에서는 타입단언은 아무런 기능을 하지 않는다. 그러므로 API 요청/응답과 같은 비동기적 코드에서 타입 단언을 쓰는 것은 에러를 발생시킨다.

실제로, 저런 방식의 코드로 인해 런타임 오류가 발생했었다.

## 3. 타입 가드

타입가드는 런타임에서의 오류까지 방지할 수 있다. TypeScript 공식 Docs에서는 Narrowing이라고 불리는데, 의미에서 유추할 수 있듯 타입을 좁혀나가는 방법이라 할 수 있다. 상기 예시코드를 타입 가드를 적용한다면 아래와 같이 표현할 수 있다.

```
const response = fetchAPI('/users') as User;

return {response !== undefined? <h1>response.name</h1> : null};
```

API응답을 답는 response는 undefined또는 User 라는 타입이 들어오게 된다. 그러므로, 삼항 연산자로 response가 값이 들어왔을 때만 렌더링을 하도록 처리했다. 이 코드는 런타임에서도 동작이 보장되므로, 에러를 방지할 수 있다.

## 4. 결론

타입 단언은 TypeScript의 깐깐한 타입 에러를 넘어가기에는 좋은 방법으로 보일 수 있다. 하지만, 이러한 조치는 깨진 독을 손으로 막는 것과 다름없다고 생각한다. 타입 가드와 같은 기법을 사용하여 런타임 에러를 방지하자. 에러라고 하여, 무조건 좋지 않은 것이 아니라 더 나은 방향을 제시하는 실마리라고 인지해야한다. 지리멸렬하고 생산성을 낮추는 것이 아닌, 견고한 애플리케이션을 만들게끔하는 이정표임을 명심하자.



## Reference

- [TypeScript](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html)
- [React](https://reactjs.org/docs/react-dom-client.html#createroot)
