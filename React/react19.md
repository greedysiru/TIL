# Fragments

* DOM에 별개의 노드를 추가하지 않고 엘리먼트들을 그룹화할 수 있는 방법



## 동기

* 특정 HTML은 부모와 자식의 종속관계가 분명할 수 있음
  * div를 사용하면 종속관계를 깨트려 렌더링이 유효하지 않음
* React.Fragment는 그룹화만을 위한 컴포넌트로 렌더링이 되지 않음

```React
const table = () => {
  return (
  	<table>
    	<tr>
        <!-- Columns 컴포넌트는 td 엘리먼트만 반환해야 함 -->
      	<Columns />
      </tr>
    </table>
  )
}

-------------------------------------------------------
  
const Columns = () => {
  return (
  	<Ract.Fragment>
    	<td>리액트</td>
      <td>예시</td>
    </Ract.Fragment>
  )
}
```



### 단축 문법

* 단, key가 존재하는 경우는 Fragment를 명시적으로 선언해야 함

```React
const Columns = () => {
  return (
  	<>
    	<td>리액트</td>
      <td>예시</td>
    </>
  )
}
```





# Reference

[React 공식 문서](https://ko.reactjs.org/)

