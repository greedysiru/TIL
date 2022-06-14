# 웹 접근성

* 모두가 사용할 수 있는 웹 사이트를 개발하는 것
* 보조과학기술(assistive technology)이 웹 사이트를 해석할 수 있도록 하는 것
  * 스크린 리더



## 1. 시맨틱 HTML

* div를 지양하고 의미가 있는 태그를 사용
  * React로 구성한 코드가 돌아기게 만들기 위해 사용하는 경우, React Fragment를 사용할 것

```React
function example() {
  return (
  	<div>
    	<dt>예시</dt>
      <dd>예시</dd>
    </div>
  )
}

-----------------------------------------------------------------
// Good
function example() {
  return (
  	<Fragment>
    	<dt>예시</dt>
      <dd>예시</dd>
    </Fragment>
  )
}
```



## 2. 라벨링

* input, textarea와 같은 HTML 폼 컨트롤은 구분할 수 있는 라벨이 필요
* jsx에서는 htmlFor로 사용하여 라벨링 할 것

```React
function example() {
  return (
    <Fragment>
      <label htmlFor="nicknameInput">닉네임을 입력하세요</label>
      <input id="nicknameInput" type="text" name="name"/>
    </Fragment>
  )
}
```



## 3. 포커스 컨트롤

* 웹 애플리케이션은 키보드만 사용하여 모든 동작을 할 수 있어야 함
* 키보드 탐색을 돕고 탐색 속도를 높일 수 있도록 영역을 건너뛸 방법을 제공해야 함
  * 이를 위해, main, aside 태그와 같은 랜드마크 엘리먼트를 사용하여 페이지 영역을 나누어야 함
* React의 경우, HTML DOM을 변경하기 때문에 포커스 컨트롤이 예상치 못하게 동작할 수 있음
  * useRef 훅을 사용하여 DOM에 포커스를 주기

```React
function example() {
  const textInput = useRef();
  
  useEffect(() => {
    // 렌더링 되었을 때 포커스
    textInput.current.focus();
  }, []);
  
  return (
    <Fragment>
      <label htmlFor="nicknameInput">닉네임을 입력하세요</label>
      <input ref={textInput} id="nicknameInput" type="text" name="name"/>
    </Fragment>
  )
}
```







# Reference

[React 공식 문서](https://ko.reactjs.org/)

