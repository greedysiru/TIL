# Part 1. FLEX, SCSS 기초(SCSS를 활용한 효율적인 CSS 관리)

## 1. SASS란?

* CSS 전처리기
* 변수, 반복문, 함수 등을 사용할 수 있음
* 실제 브라우저가 SASS를 읽을 수는 없음
  * **CSS 파일로 변환해야 함**
* SCSS
  * SASS의 한 버전
  * 원래 SASS는 중괄호가 없어 가독성이 떨어지므로 중괄호가 있는 SCSS를 사용



## 2. SASS -> CSS 변환

1. npm에서 sass install

```shell
npm install -g sass
```

2. sass 또는 scss를 css로 변환

```shell
sass --watch example.scss:example.css
```





## 3. Variable

* `$` prefix를 붙여야 함
* 자주 사용되는 공통적인 값을 변수로 선언하면 유용

```scss
$defaultColor: #fff

.box {
  width: 100px;
  height: 100px;
  backgrouond-color: $defaultColor;
}
```



## 4. import

* 부분 파일(partial file)의 네이밍은 _(under bar)로 시작
  * ex) _reset.scss
  * import시, _(under bar)와 확장자는 생략
* import한 파일의 변수 또한 사용할 수 있음

```scss
// src/_reset.scss
* {margin:0px; padding:0px;}
ul,ol {list-style:none;}
a {text-decoration:none;}

// src/_fonts.scss
$titleFont: 'orbitron';
$contentFont: 'arial';

$fontBig: 30px;
$fontMid: 16px;
$fontSmall: 12px;

// src/style.scss
@import 'reset';
@import 'fonts';

h1 {
  font-size: $fontBig;
  font-family: $titleFont;
}
```



## 5. Nesting

* HTML 구조대로 선택자를 Nesting할 수 있음
* &키워드와 Nesting을 활용하여 가상 선택자를 접근할 수 있음

```HTML
<body>
  <div class="item">
    
  </div>
</body>
```

```scss
body {
  // ...
  .item {
    // ...
    
    // item class가 hover되었을 때의 스타일링 지정
    &:hover {
      // ..
    }
  }
}
```



## 6. Mixin

* 스타일링의 틀을 함수처럼 정의해서 사용
  * parameter를 정의하여 사용하는 쪽에서 인자를 넘겨 스타일링 가능
* default parameter를 정의 가능
* 사용하는 쪽에서 특정 parameter만 넘기기 가능

```scss
// src/_mixin.scss
@mixin button ($wid: 80px, $ht: 30px, $bgColor: aqua, $color: #fff, $fontSize: 12px, $corner: 0px){
  color: $color;
  font-size: $fontSize;
  display: block;
  width: $wid;
  height: $ht;
  background: $bgColor;
  text-align: center;
  line-height: $ht;
  border-radius: $corner;
}

// src/style.scss
@import 'mixin';

a {
  @include button(80px, 30px, aqua, #fff, 12px, 0px);
}

span {
  @include button($cornder: 20px);
}
```



## 7. @for

* 반복문 기능을 사용 가능
* @for 변수 from 시작하는수 through(또는 to) 끝나는수
  * through의 경우 끝나는 수를 포함
  * to의 경우 끝나는 수를 포함하지 않음
  * for문 안의 선택자에서 변수를 사용할 때는 #{}로 감싸주기

```html
<div class="wrap">
  <div class="item">
    ...
  </div>
</div>
```

```scss
.wrap {
  width: 100%;
  border: 2px solid #bbb;
  box-sizing: border-box;
  padding: 100px;
  
  .item {
    opacity: 0;
    transform: translateY(100px);
    transition-duration: 0.5s;
    
    // 1부터 4까지 반복하고 그 수를 $i에 할당
    @for $i from 1 through 4 {
      // ${}로 변수를 감싸기
      &:nth-of-type(#{$i}) {
      	transition-delay: 0.1s * $i;
    	}
    }
  }
    &:hover {
    .item {
      opacity: 1;
      transform: translateY(0px);
    }
  }
}
```

