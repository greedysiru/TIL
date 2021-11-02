

# Flex Layout

**본 내용은 10분 테코톡 콜린님의 강의를 토대로 작성하였습니다.**

## 1. Layout
* HTML, CSS에서 레이아웃이란 문서 위에 상자를 적절한 위치에 배치하는 방법을 의미

### nomal flow
* 브라우저 기본값으로 HTML 페이지를 배치하는 방법
* block, inline 두 가지의 방법 존재
* nomal flow로만 화면을 구성하는 것에는 한계가 있음
* CSS의 적절한 스타일과 레이아웃을 조절하는 방법을 통해 사용자가 정보를 습득하기 편리하 형태로 변경해야 함

### block
* 자신의 부모요소 너비를 전부 차지
* 새로운 블록을 추가할 시, 다음 라인에 개행되어 추가

### inline
* 컨텐츠 영역만큼만 너비 차지
* 부모의 최대 너비까지 나란히 위치
* 부모의 너비를 넘긴 경우, 개행하여 배치

## 2. Flex 용어
### flex
* 요소들을 행, 열 단위로 정렬하기 위한 1차원 레이아웃
* 간단한 레이아웃에 좋음, 복잡한 레이아웃은 grid 권장
* 부모의 요소에 **display: flex** 지정
```CSS
.parent {
  display: flex;
}
```

### flex 용어
* flex container: flex item들의 배치나 정렬을 담당하는 역할, 속성값들을 활용
  * flex-direction
  * flex-wrap
  * justify-content
  * align-items
  * align-content
* flex item: flex container의 자식 요소에 해당하는 요소
  * flex
  * flex-flow
  * flex-shrink
  * flex-basis
  * order
  * align-self
* main axis: flex item들의 주요 배치 방법과 정렬 등의 기준점이 되는 축, 주축
  * main start를 기점으로 main end 방향으로 아이템들이 배치
* cross axis: flex item들의 부차적인 정렬에 대한 기준을 담당
  * cross start를 기점으로 cross end 방향 기준 정렬 가능

## 3. Flex 속성(container)
### flex-direction
* main axis 방향을 결정하는 속성
* row: main 축이 row 방향으로 설정, item들이 row 방향 기준으로 나열(가로)
* column: main 축이 column 방향으로 설정, item들이 column 방향 기준으로 나열(세로)
* -reverse: main 시작점이 반대방향에서 시작하는 구조



### writing mode & direction

* 문서 내 요소들이 배치되는 흐름은 wrting-mode, direction 속성과 관련

```CSS
writing-mode: horizontal-tb; /* horizontal top bottom(default) */
direction: ltr; /* left to right(default) */
writing-mode: vertical-lr; /* vertical left right */
direction: rtl; /* right to left */
```



### flex-wrap

* item이 컨테이너의 영역을 overflow 했을 때의 배치
* nowrap(default): 부모의 너비를 overflow하더라도 한 개의 라인을 유지
* wrap: overflow시에 새로운 줄로 대치
* wrap-reverse



### justify-content

* main axis 기준으로 item들을 정렬
* center: main axis 기준으로 중앙
* space-between: main axis 기준으로 동일한 간격을 두어 위치



### align-items

* cross axis를 기준으로 item들을 정렬
* stretch
* center: cross axis를 기준으로 중앙에 위치



## 4. Flex 속성(item)

### order

* flex-item의 시각적 순서를 변경하는 속성
* 음수: main-start 쪽(순서상 앞)
* 0: default
* 양수: main-end 쪽(순서상 뒤)
* 모든 접속 환경에서 동일한 문서구조를 가져가지만, 접속 환경에 따라 시각적으로 다르게 보여주고 싶을 때



### 크기 조절

* flex-item의 크기를 조절하는 속성
* 기본 크기 또는 늘리거나 줄일 비율을 설정
* flex-grow: 늘어날 비율을 결정하는 속성
  * container의 빈 공간을 비율에 따라 분배하는 방식으로 결정
  * 0: default, 빈 영억을 채우지 않음, item 크기가 늘어나지 않음
  * 숫자: 비율
* flex-shrink
  * flex-item이 줄어드는 비율을 결정하는 속성
  * 0: item 크기가 줄어들지 않음
  * 숫자: 비율, 1(default)
* flex-basis: flex-item의 기본 크기를 설정
  * auto: default, 컨텐츠를 차지하는 영역
  * 값: px, %, rem, em
* flex
  * flex-grow, flex-shrink, flex-basis의 축약형 속성



### 크기 조절 예시

1. 컨테이너 영역의 빈 영역 크기를 구함
2. 아이템들의 flex-grow 합을 구함
3. 빈 영역의 크기 / flex-grow 합을 적절하게 분배



### gap

* flex-item 사이의 간격을 설정하는 속성
* column-gap
* row-gap



### 우선순위

* flex-basis: auto => width > flex-basis
* flex-basis: auto가 아닌 값 => flex-basis
* min(max)-width가 존재한다면 우선수위 제일 높음


# Reference

[[10분 테코톡] 콜린의 Flex Layout](https://www.youtube.com/watch?v=JQ0jO3B43YQ)
