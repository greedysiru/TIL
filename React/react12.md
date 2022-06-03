# 리스트와 Key

## 여러개의 컴포넌트 렌더링 하기

* 자바스크립트 배열의 프로토타입 메서드 중 하나인 map과 JSX를 활용하여 여러개의 컴포넌트 렌더링 가능
* key: 엘리먼트 리스트를 만들 떄 포함해야 하는 특수한 문자열 어트리뷰트
  * 어떤 항목을 변경, 추가, 삭제할 지 식별하는 것을 도움
  * 엘리먼트에 안정적인 고유성 부여
  * 배열의 인덱스보다는 식별할 수 있는 문자열을 사용하기
  * map 내부의 엘리먼트에서 key를 넣어줄 것
  * 형제 사이에서 고유하면 됨



### 연속된 li 엘리먼트 렌더링하기

```React
...
// 각 요소별로 고양이에 대한 정보 객체를 가지는 배열
const cats = [
  {name: 'siru', age: 7},
  {name: 'nunu', age: 6},
  {name: 'mango', age: 7},
  {name: 'meonji', age: 4},
];

// 각 요소를 li 태그에 표현
cats.map((item, index) => {
  // 각 아이템에 대해 식별하기 위한 고유한 문자열
  const uniqueID = `${item.name}-${index}`;
  // 각 요소에 대한 정보를 li 태그 안에 표현
  return <li key={uniqueID}>이름 :{item.name} / 나이: {item.age}</li>
});
```

# Reference

[React 공식 문서](https://ko.reactjs.org/)

