# Part 1. FLEX, SCSS 기초(Flex의 기본 문법)

* flex는 자식을 감싸고 있는 부모(layout)에 설정
  * `display: flex`
* 기본적으로 가로 방향으로 배치 됨



## 1. 기본축 배치

* `justify-content`
  * flex-start: 시작부터 배치
  * flex-end: 끝부터 배치
  * center: 가운데 배치
  * space-between: 자식들을 자식간 사이에만 여유 공간을 두고 배치
  * space-around: 자식들을 앞, 뒤, 자식간 사이에 여유공간을 두고 배치
  * space-evenly: 자식들을 앞, 뒤, 자식간 사이에 여유공간을 두고 균등하게 배치(홀수인 경우에도)

```HTML
<body>
  <section>
  	<article>1</article>
    <article>2</article>
    <article>3</article>
  </section>
</body>
```

```SCSS
section {
  ...
  // 부모에 flex 설정
  display: flex;
  // flex 가로축의 배치 설정
  justify-content: center;
  
  article {
    ...
  }
}
```



## 2. 수직축 배치

* `align-items`
  * 모든 속성값은 `justify-content`와 동일
  * flex-start: 시작부터 배치
  * flex-end: 끝부터 배치
  * center: 가운데 배치
  * space-between: 자식들을 자식간 사이에만 여유 공간을 두고 배치
  * space-around: 자식들을 앞, 뒤, 자식간 사이에 여유공간을 두고 배치
  * space-evenly: 자식들을 앞, 뒤, 자식간 사이에 여유공간을 두고 균등하게 배치(홀수인 경우에도)
* `align-content`
  * 줄바꿈이 되었을 때 수직축 배치
  * 줄바꿈이 될 상황에서는 이 속성을 정의하기
  * 모든 속성값은 위와 동일



## 3. 줄바꿈 설정

* flex에서는 부모 요소가 줄어들어, 줄바꿈이 되지 않고 자식들 크기가 줄어듦
* `flex-wrap: wrap` 을 적용



## 4. 기본축 변경

* `flex-direction`

  * 자식들을 배치하는 방향

  * row: 기본값, 행으로 배치(가로)

  * column: 열로 배치(세로)
  * column-reverse: 자식들을 반대 순서로 열 배치(세로)

  * 이 설정에 따라 요소가 나열된 축을 기본축, 수직으로 된 축을 수직축이라고 칭함



## 5. flex-flow

* `flex-direction` 과 `flex-wrap`을 동시에 정의할 수 있음

```SCSS
.layout {
  flex-flow: row wrap;
}
```



## 6. 박스의 비율 및 순서 변경

### flex

* 레이아웃이 flex인 자식 요소들의 너비 값을 균등하게 정의할 수 있음
* `flex`
  * 첫번째 속성 값은 비율
  * 두번째 속성 값은 기본 크기



```HTML
<body>
  <section>
  	<article>1</article>
    <article>2</article>
    <article>3</article>
  </section>
</body>
```

```SCSS
section {
  ...
  // 부모에 flex 설정
  display: flex;
  // flex 가로축의 배치 설정
  justify-content: center;
  
  article {
    ...
    height: 100px;
    // 각 자식 요소가 1의 비율로 균등하게 너비를 차지
    // 요소가 세개 이므로 1:1:1
    flex: 1;
  }
}

// 특정 요소의 비율만 다르게 하는 경우
section {
  ...
  // 부모에 flex 설정
  display: flex;
  // flex 가로축의 배치 설정
  justify-content: center;
  
  article {
    ...
    height: 100px;
    // 각 자식 요소가 1의 비율로 정의
    flex: 1;
    
    // 1:2:1 비율로 너비가 적용 됨
    &:nth-of-type(2) {
      flex: 3;
    }
  }
}
```



### order

* 자식의 순서를 바꿀 수 있음
* DOM의 구조를 바꾸는 것이 아닌 화면에 보이는 정렬 방식을 바꾸는 것

```SCSS
article {
  // 첫번째 자식이 두번째로 정렬 됨
  &:nth-of-type(1) {
    order: 2;
  }
}
```

