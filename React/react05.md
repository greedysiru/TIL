# Virtual DOM

**본 내용은 10분 테코톡 지그님의 강의를 토대로 작성하였습니다.**



## 1. 브라우저의 동작

### 브라우저 렌더링 과정

> **DOM tree 생성 ->**
>
> **render tree 생성 ->**
>
> **Layout (reflow) ->**
>
> **Paint (repaint)**



### DOM 조작의 비효율성

* **어떤 상호작용에 의해 DOM에 변화가 발생하면 render tree가 그때마다 재생성된다.**
* 변화가 발생하면 모든 요소들의 스타일을 다시 계산하고 Layout (reflow) 과정을 거쳐 repaint하는 과정까지 반복
* 좋아요를 누르거나, 장바구니 목록에서 상품을 삭제하거나, 댓글을 남기면 **전체 노드들이 처음부터 다시 그려진다.**



## 2. Virtual DOM의 등장

### Virtual DOM의 등장

* SPA를 많이 사용하면서, **DOM tree를 즉각적으로 변경할 상황**이 많이 생김
* 브라우저단에서 **JavaScript가 관리**하기 때문에 DOM조작을 더욱 더 효율적으로 할 수 있도록 **최적화가 필요**해짐



### virtual DOM이란?

* DOM의 복사본
* HTML DOM의 추상화 버전
* 실제 DOM과 같은 속성을 가지지만, api를 가지고 있지는 않음



### Virtual DOM의 동작 원리

* 데이터가 변경되면 전체 UI는 Virtual DOM에 렌더링
* 이전 Virtual DOM에 있던 내용과 업데이트 후에 내용을 비교하여 바뀐 부분만 실제 DOM에 적용
* 원본 DOM에 필요한 변화만 반영
* 필요한 UI의 업데이트를 적용할 수 있다.
* 실제 DOM이 아닌 메모리 상에서 동작하므로 빠르게 동작
* 실제 렌더링이 되지 않아 연산비용이 적음
* 모든 변화를 하나로 묶어서 한 번만 실행
* **DOM fragment의 변화를 묶어 적용 후 기존 DOM에 던져주는 과정을 자동화 & 추상화**



### Virtual DOM의 생김새

* HTML 객체에 기반한 자바스크립트 객체로 표현됨

```HTML
<ul id="itmes">
  <li>Item 1</li>
  <lt>Item 2</lt>
</ul>
```

```JavaScript
let domNode = {
  tagName: "ul",
  attributes: { id: "items" },
  children: [
    {
      tagName: "li",
      textContent: "Item 1",
    },
    {
      tagName: "li",
      textContent: "Item 2",
    },
  ],
};
```





## 3. React의 Virtual DOM

* Virtual DOM을 이용하는 대표적인 JavaScript 라이브러리
* **재조정**
  * **UI의 가상적인 표현을 메모리에 저장하고, ReactDOM과 같은 라이브러리에 의해 실제 DOM과 동기화**



### JSX

* 각 컴포넌트에서 return되는 react element를 표현하는 문법
* JavaScript 확장 문법
* JSX를 컴포넌트에서 return시키면 Babel은 **React.createElement() 호출**로 컴파일
* 생성된 **React Elements**는 내부적으로 **객체**로 표현 (Virtual DOM의 객체 구성 형태와 비슷)
  * light, immutable, stateless. **가볍고 상태를 가지지 않으며 불변성을 유지**
* React Elements는 render에 의해서 실제 DOM 요소가 된다.
* React는 객체를 읽어들이고 이를 사용해서 DOM을 구성, 최신 상태를 유지한다.
* 각 element는 해당 순간의 UI를 스냅샷 형태로 보여준다.
* UI 업데이트는 새로운 요소를 만들어 render로 전송한다.
  * Virtual DOM



### Diffing

* 모든 React DOM Object에는 그에 대응하는 **Virtual DOM Object**가 있다.
* **Virtual DOM Object**는 **DOM Object**를 대신한다.
* Virtual DOM object는 DOM Object 하나하나에 매핑
* 데이터가 업데이트 되면, 바뀐 데이터를 바탕으로 **React.createElement()**를 통해 JSX Element를 렌더링
* 모든 각각의 Virtual DOM Object가 업데이트 된다.
  * 빠르게 업데이트 되기 때문에 비용이 많이 들지 않음
* Virtual DOM이 업데이트되면 React는 Virtual DOM을 업데이트 이전의 스냅샷과 비교하여 정확히 어떤 Virtual DOM이 바뀌었는지 검사(Diffing)
  * element의 속성 값만 변한 경우에는 속성 값만 업데이트
  * element의 태그 또는 컴포넌트가 변경된 경우 해당 노드를 포함한 하위의 모든 노드를 unmount 후 새로운 virtual DOM으로 대체
  * 이런 변경, 업데이트가 모두 마무리 된 이후에 실제 DOM에 결과를 업데이트



### Diffing 요약

1. 전제 Virtual DOM이 업데이트
2. Virtual DOM을 업데이트 이전의 시점과 비교
3. 실제로 바뀐 부분만 real DOM에서 바꿈
4. real DOM의 변화가 스크린에 그려진다.



## 4. 정리

* 무조건 Virtual DOM이 빠르진 않다.
  * 정보 제공만 하는 웹페이지라면 상호작용이 없으므로 일반 DOM 성능이 좋을 수도 있다.
* SPA로 제작된 큰 규모의 웹페이지에서는 Virtual DOM이 브라우저 연산 양을 줄여 성능을 개선할 수 있다.

# Reference

[[10분 테코톡] 카일의 프론트엔드의 비동기](https://www.youtube.com/watch?v=PN_WmsgbQCo&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=13)

​	