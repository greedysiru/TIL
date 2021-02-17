# [코드잇] HTML/CSS 핵심개념 (2)(2021.2.17)



**상세 내용 [블로그](https://greedysiru.tistory.com/210?category=860702) 참고**



# CSS 제대로 활용하기

## 01. 선택자 정리

* **선택자 : CSS에서 스타일링할 요소**



### 태그 이름

```CSS
h1 {
  color: red;
}
```



### 클래스/아이디

```CSS
.title {
  color: red;
}

#important {
  color: white;
}
```



### 자식 (children)

* 부모 요소의 해당 모든 자식 요소에 스타일 적용

```CSS
.title span {
  color: orange;
}
```



### 직속 자식 (direct children)

* 부모요소의 해당 직속 자식 요소에만 스타일 적용

```CSS
.title > span {
  color: whitesmoke;
}
```



### 복수 선택

* 콤마로 구분

```CSS
.title, #subtitle {
  color: teal;
}
```



### 여러 조건

```CSS
.outside .title {
  color: white;
}
```



## 02. 가상 클래스 (Pseudo- class)

* **콜론(:)을 사용하면 가상 클래스를 선택**



### n번째 자식

```CSS
div:firsht-child{
  color: blue;
}
div:nth-child(3){
  color: red;
}
div:last-child{
  color: white;
}

/* 마지막 자식이 아닌 것 */
div:not(:last-child){
  font-size: 30px;
}
```



### 마우스 오버(hover)

마우스가 해당 요소에 올라갔을 때

```CSS
a:hover {
  color: teal;
}
```



## 03. CSS 상속

* **부모 요소의 속성들을 자식들에게 넘겨주는 것**



### 상속되는 속성들

1. **color**
2. **font-family**
3. **font-size**
4. **font-weight**
5. **line-height**
6. **list-style**
7. **text-align**
8. **visibility**

위의 속성들이 항상 상속되는 것은 아니다. **a 태그의 경우 color가 상속되지 않는다.** 해당 **속성 값에 inherit을 사용**하면 상속이 된다.



## 04. CSS 우선 순위

### 순서

* 똑같은 선택자가 있으면, 이전에 나온 스타일을 덮어쓴다.

```CSS
h1 {
  color: blue;
  text-align: center;
}

h1 {
  color: green;
}
```



### 명시도 (Specificity)

같은 요소를 가리키지만, 선택자가 다르면 **명시도에 따라 우선 순위가 결정**

1. 인라인 스타일이 가장 우선 순위가 높다.
2. 선택자에 id가 많을 수록 우선 순위가 높다.
3. 선택자에 class, attribute, pseudo-class가 많을 수록 우선 순위가 높다.
4. 그 다음은 요소(또는 가상 요소)가 많은 순서이다.



## 06. CSS의 다양한 단위들

### px

* 절대적인 값
* 다른 요소의 값에 영향을 받지 않는다.



### rem

* 상대적인 값
* **오직 html태그의 font-size에만 영향을 받는다.**



### em

* 상대적인 값
* 자기 자신의 font-size를 기준으로 한다.
* **자기 자신의 font-size를 정해주지 않으면, 상위 요소에서 상속받은 값을 기준으로 한다.**



### 퍼센트(%)

* 상대적인 값
* **상위 요소의 font-size에 곱해주는 방식**
* **margin, padding의 단위로 사용되는 경우, 상위 요소의 width를 기준으로 계산**
  * margin-top, padding-bottom의 경우도 width를 기준으로 계산

# Reference

[코드잇 - HTML/CSS 시작하기](https://www.codeit.kr/courses/web-publishing)

