# 클린코드 자바스크립트 - 배열 다루기(배열 요소에 접근하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 배열 요소에 접근하기

* element: 배열 하나하나의 요소



### 구조분해 할당으로 접근하기

* 인덱스로 접근하는 것보다 구조분해 할당으로 접근하는 것이 더 명시적

```JavaScript
const [firstCat, secondCat] = cats;

// 위 문법은 react.js에서도 많이 사용되는 문법
const [value, setValue] = useState();
```



### 전달받은 파라미터를 구조분해하기

* 함수의 경우, 전달받은 파라미터를 구조분해하여 명시적이고 간결하게 접근할 수 있음

```JavaScript
const callCats = ([firstCat, secondCats]) => console.log(firstCat, secondCat);

callCats(['siru', 'nunu']);
```



### DOM API에서 구조분해 할당 활용하기

* 구조분해 할당을 활용하여 여러 요소를 DOM API로 가져왔을 때, 각 요소를 명시적으로 표현

```JavaScript
// 인덱스로 접근하기
const getButtons = () => {
  const buttons = document.getElementByTagName('button');
  // 각각 변수에 담지만, 명시적인 방법이 아니고 효율적이지 않음
  const confirmButton = buttons[0];
  const cancleButton = buttons[1];
  const resetButton = buttons[2];
}

// 구조분해 할당
const getButtons = () => {
  // 명시적으로 리팩터링
  const [confirmButton, cancleButton, resetButton] = document.getElementByTagName('button');
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)