# [노마드코더]코코아톡 클론코딩 (4)(2021.1.6)



**상세 내용 [블로그](https://greedysiru.tistory.com/96) 참고**



# Advanced CSS

## 1. Transitions

* **transitions는 state가 없는 요소에 붙어야 한다.**
* **state**에 들어있는 것을 기준으로 애니메이션 효과를 준다

```CSS
<head>    
    <style>
        a {
            color: wheat;
            background-color: tomato;
            text-decoration: none;
            padding: 3px 5px;
            border-radius: 5px;
            font-size: 55px;
            transition:
              background-color 1s ease-in-out,
              color 1s ease-in-out,
              border-radius 1s ease-in-out;
          } /* all 5s ease-in-out */
        a:hover {
            border-radius: 15px;
            color:tomato;
            background-color: wheat;
        }
    </style>
</head>

<body>
    <a href="#">Go home</a>
</body>
```

* **a:hover**에서 변경되는 것들을 기준으로 애니메이션 효과가 적용
* **color 1s ease-in-out**
  * 적용할 속성, 시간, 변화하는 방법 순으로 쓴다

## 2. Transformations

* 한 요소를 원하는대로 변형
* matrix, rotate, scale 등
* Box element를 변형하지 않는다.
  * margin, padding이 적용되지 않는다.
* 옆의 요소에게 영향을 끼치지 않는다.

```CSS
<head>
    <style>
        img {
            border: 5px solid black;
            border-radius: 50%;
            transition:  transform 2s ease-in-out;
        }
        img:hover {
            transform: rotate(360deg) scale(0.5);
        }
    </style>
</head>
<body>
    <img src="img/anything.png"/>
</body>
```

* **transform: rotate(360deg) scale(0.5)**
  * 회전과 작아지는 효과



## 3. Animations

*  Animation 효과

```CSS
<head>
    <style>
        @keyframes superSexyCoinFlip{
            from{
                transform: rotateY(0);
            }
            to{
                transform: rotateY(180deg);
            }
        }
        img {
            border: 10px solid black;
            border-radius: 50%;
            animation: superSexyCoinFlip 5s ease-in-out infinite;
        }

    </style>
</head>

<body>
    <img src="img/anything.png"/>
</body>
```

* **@keyframes** 뒤에 Animation의 이름을 적는다.
* **form**에서 **to**로 효과를 적용한다.
* 적용할 요소 안에 **animation:**뒤에 설정한 Animation의 이름을 적어준다.
  * **infinite**는 무한 반복
* 아래처럼, 단계를 더 세분화

```CSS
<head>
<style>
        @keyframes superSexyCoinFlip{
            0% {
                transform: rotateY(0);
            }
            50% {
                transform: rotateY(180deg) translateY(100px);
            }
            100% {
                transform: rotateY(0);
            }
        }
        img {
            border: 10px solid black;
            border-radius: 50%;
            width: 200px;
            animation: superSexyCoinFlip 5s ease-in-out infinite;
        }

    </style>
</head>
<body>
    <img src="img/anything.png"/>
</body>
```



## 4. Media Queries

```CSS
<head>
    <style>
        body {
            display: flex;
            height: 100vh;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }
        div {
            background-color: teal;
            width: 200px;
            height: 200px;
        }
        @media screen and (max-width: 600px) {
            div {
                background-color: tomato;
            }
        }
        @media screen and (min-width: 601px) and (max-width: 1200px) {
            div {
                background-color: wheat;
            }
        }
        @media screen and (min-width: 1200px) {
            div {
                background-color: turquoise;
            }
        }
        span {
            font-size: 36px;
        }
        @media screen and (orientation: landscape) {
            span {
                display: none;
            }

        }
    </style>
</head>
<body>
    <div></div>
    <span>Please flip your phone</span>
</body>
```

* **@media **로 media query호출한 뒤 조건을 입력
  * 조건이 **참**일 때 CSS를 실행
  * 괄호를 열고 안에 요소를 적어야한다.
  * **screen** : 우리가 보는 스크린에 적용한다는 의미
    * **print** : 인쇄 환경에서의 출력
  * **and**를 써서 연결된다.
  * max : 숫자보다 작을 때
  * min: 숫자보다 클 때
  * **min-device-width** : 모바일 환경에서의 조건
  * **orientation : landscape**로 가로모드일 때 출력 조건을 입력할 수 있다.
    * **portrait** : 세로모드



# Reference

https://nomadcoders.co/kokoa-clone/lobby