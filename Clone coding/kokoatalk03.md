# [노마드코더]코코아톡 클론코딩 (3)(2021.1.5)



**상세 내용 [블로그](https://greedysiru.tistory.com/94) 참고**



# Learning CSS

## 1. Flexbox

* **Flexbox**는 반응형 디자인을 지원

```CSS
<head>
<style>
    body{
        height: 100vh;
        margin: 20px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>
</head>
<body>
		<div></div>
		<div></div>
		<div></div>
</body>
```

1. 부모 엘리먼트를 felx container로 만들어야 한다.
2. **justify-content** : main axis의 설정(가로,기본값)
3. **aling-items** : cross axis의 설정(세로,기본값)
4. **body**가 height가 기본값이면, align-items를 사용해도 그대로인 것처럼 보인다.

* **vh** : viewport height. 기기에 따라 달라지는 단위. 지금 화면의 %.
* 자식 엘리먼트가 컨텐츠를 포함한 경우, **Flexbox**로 설정할 수 있다.



### Flexbox의 속성

```CSS
<head>
<style>
    body{
        display: flex;
        justify-content: space-between;
        flex-direction: column-reverse;
        flex-wrap: wrap-reverse;
        align-items: center;
    }
</style>
</head>
<body>
		<div></div>
		<div></div>
		<div></div>
</body>
```

* **flex-direction**의 디폴트는 row이다.
  * **column**을 주면, main axis와 cross axis가 바뀐다.
  * **reverse**는 순서를 반대로 한다.
* **flex-wrap**
  * **wrap** 이면, 한 줄에 컨텐츠가 나올 수 있는 만큼 보여주고 나머지는 다음줄로 넘긴다.
  * **no wrap**이면, 한 줄에 모든 컨텐츠를 보여준다. (크기를 줄여서라도)
  * **reverse**는 wrapping을 할 때, 순서를 반대로 한다.



## 2. Position

* Position은 컨텐츠의 위치를 설정
* absolute, relative, fixed, static(defalut)



### fixed

* 특정 컨텐츠를 화면에 고정

```CSS
<head>
<style>
      #different {
        top: 5px;
        left: 200px;
        position: fixed;
        background-color: wheat;
        width: 350px;
      }
</style>
</head>
<body>
    <div></div>
    <div id="different"></div>
</body>
```

* **id=different**인 **div**는 **position: fixed** 속성이 주어져서 스크롤이 되어도 항상 제자리
* **top, left, right, bottom** 중에 하나가 값이 입력 되면, 해당하는 요소는 다른 레이어에 위치



### relative, absolute

#### relative

* element가 처음 만들어진 위치를 기준으로 top, bottom, left, right를 px단위로 설정



#### absolute

* 가장 가까운 **relative**를 기준으로 설정
  * 기본값은 **body**를 기준
  * **body**안에 있는 박스중 **relative**가 있다면, 그 박스를 기준으로 위치를 결정

```CSS
<style>
    div {
        width: 300px;
        height: 300px;
        background-color: wheat;
        color: white;
        position: relative;
    }
    .green{
        background-color: teal;
        height: 100px;
        width: 100px;
        position: absolute;
        top: -10px;
        left: -10px;
    }
</style>
</head>
<body>
    <div>
        <div class="green">

        </div>
    </div>
</body>
</html>
```

* **class = "green"**은 **position: absolute**
  * **div**가 **relative**이므로 이것을 기준으로 위치



## 3. Pseudo Selectors

* 특정 요소만 지정해서 설정할 수 있다.

```CSS
<head>    
<style>
    div:first-child{
        background-color: tomato;
    }
    div:last-child{
        background-color: teal;
    }
</style>
</head>
<body>
	<div></div>
	<div></div>
	<div></div>
	<div></div>
</body>
```

* 선택자 뒤의 **first-child**와 **last-child**를 지정해서, **div**의 첫 번째와 마지막만 속성을 적용



### n번째 태그 수정하기

```CSS
<head>
<style> 
    span:nth-child(2){
        background-color: teal;
    }
    span:nth-child(even){
        background-color: tomato;
    }
    span:nth-child(odd){
        background-color: whitesmoke;
    }
    span:nth-child(5n + 1){
        background-color: teal;
    }
</style>
</head>
<body>
    <span>hi</span>
    <span>hi</span>
    <span>hi</span>
    <span>hi</span>
    <span>hi</span>
    <span>hi</span>
    <span>hi</span>
</body>
```

* **nth-child(n)** : n번 째 태그를 가르킬 수 있다.
  * **even, odd** : 짝수, 홀수를 가르킬 수 있다.
  * **5n+1** : 1, 6, 11, 16... 번 째 태그를 가르킬 수 있다.



### more pseudo selctors

```CSS
<head>
<style>
    input {
        border:1px solid wheat;
    }
    input:required {
        border:1px solid tomato;
    }
    input[type="password"]{
        background-color: thistle;
    }
    input[placeholder~="name"]{
        background-color: pink;
    }
</style>
</head>
<body>
    <div>
        <form>
            <input type="text" placeholder="Frist name"/>
            <input type="text" placeholder="Last name"/>
            <input type="password" required placeholder="password"/>
        </form>
    </div>
</body>
```

* **input:required** : **input**태그 중에서 **required**인 요소를 적용
* **input[type="password"]** : **input**태그 중에서 **type=password**인 요소를 적용
* **input[placeholder~="name"]** : **input**태그 중에서 **placeholder**에 **name**이 포함하는 것을 적용 



### pseudo element

* **::placeholder**
  * **placeholder**를 설정할 수 있다.
* **::selection**
  * 드래그했을 때 효과를 설정
* **::firstletter**
  * 첫 문자만 꾸미기
* **::first line**
  * 첫 줄만 꾸미기



## 4. Combinators

* 부모, 자식 elements 관계를 이용해서 스타일을 적용

```CSS
<head>
<style>
    span {
        background-color: yellowgreen;
        padding:5px;
        border-radius: 10px;
    }
    p span{
        color:white;
    }
    div > span{
        text-decoration: underline;
    }
    p + span{
        text-decoration: underline;
    }
</style>
</head>
<body>
    <div>
        <span>hello</span>
        <p>
        hello, I'm greedysiru! <span>jaemin</span>
        </p>
        <span>GOOD</span>
    </div>

</body>
```

* **p span** : p태그(부모) 하위의 **모든** span태그(자식)에 스타일을 적용
* **div > span** : div태그(부모) **바로 하위**(자식)의 span태그에만 스타일을 적용.
* **p + span**  : p태그 **다음 순서**(형제)의 span에 스타일을 적용
  * **P ~ span** : 형제인데, 바로 뒤에 오지 않을 때



## 5. States

* 요소가 특정 조건으로 활성화 되었을 때, 효과를 줄 수 있다.
* active : 해당 요소를 마우스로 클릭했을 때 효과 적용
* hover : 마우스가 해당 요소 위를  지나갈 때 효과 적용
* focus : 키보드로 선택되었을 때 효과 적용
* focus-within : 부모 요소에게 적용. 하위 요소가 선택되었을 때, 효과를 적용
* visited : 방문한 사이트일 경우에 효과 적용
* 여러 조건 하에서 효과를 적용시킬 수도 있다.

```CSS
<style>
<head>
    form:hover input:focus{
        background-color: violet;
    }
</style>
</head>
<body>
    <form>
        <input type="text">
        <input type="text">
        <input type="text">
    </form>   
</body>
```

* **form : hover input : focus** : form에 마우스가 올려져 있고 input이 focused되었을 때, 효과 적용



## 6. Colors and Variables

### Colors

CSS에서 사용하는 색 체계는 아래와 같다.

1. hexadecimal color (16진수 컬러)
   * #000000 방식으로 표현
2. RGB 방식
   * 디자이너들이 많이 사용하는 방법
   * RGB(0,0,0) 방식으로 표현
   * Red, Green, Blue의 삼원색을 사용
3. RGBA 방식
   * RGB에 투명도를 더한 방식



### Variable (custom properties)

* 변수에 지정하고 싶은 색상 코드나 설정을 선언

```CSS
<head>
<style>
    :root {
        --main-color: #fcce00;
        --default-border: 1px solid var(--main-color);
    }
    p {
        background-color: var(--main-color);
    }
    a {
        color: var(--main-color);
        border: var(--default-border);
    }
</style>
</head>
<body>
    <p>
        가나다
    </p>
    <a href="http://www.naver.com">go to naver</a>
</body>
```

* **:root**라는 element에 변수를 추가
  * 변수명은 **--**을 먼저 써야 한다.
  * 공백은 **-**으로 채운다.
* 변수 사용은 **var**를 붙인다.



# Reference

https://nomadcoders.co/kokoa-clone/lobby