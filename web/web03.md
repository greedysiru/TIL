# [스파르타코딩] 웹개발 종합반 항해 1기 2주차 (1)(2021.2.2)



**상세 내용 [블로그](https://greedysiru.tistory.com/157?category=875936) 참고**



# 1. JQuery 시작하기

* HTML의 요소들을 조작하는 Javascript 코드를 미리 작성해둔 것 : **라이브러리**
* 복잡한 코드, 브라우저간의 호환성을 극복
* 미리 짜둔 코드이기 때문에, 사용전에 **import**해야한다.



# 2. JQuery 다뤄보기

## import

* Jquery를 사용하기 위해, 항상 **import**를 먼저 한다.

```html
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
</head>
```



## 자주 사용하는 JQuery

### input 박스의 값 가져오기

```HTML
<div class="posting-box">
    <div class="form-group">
        <label for="exampleInputEmail1">아티클 URL</label>
        <input id="post-url" type="email" class="form-control" aria-describedby="emailHelp" <!-- id 지정 -->
            placeholder="">
    </div>
    <div class="form-group">
        <label for="exampleInputPassword1">간단 코멘트</label>
        <input type="password" class="form-control" placeholder="">
    </div>
    <button type="submit" class="btn btn-primary">기사 저장</button>
</div>
```

* 크롬 콘솔창에서

```Javascript
$('#post-url').val();
// id가 post-url인 inputbox에 접근한다.
// val() 괄호 안에 값을 입력하면 inputbox의 텍스트를 입력할 수 있다.
```



### div 보이기 / 숨기기

```HTML
<div class="posting-box" id="post-box"> <!-- id 지정 -->
    <div class="form-group">
        <label for="exampleInputEmail1">아티클 URL</label>
        <input id="post-url" type="email" class="form-control" aria-describedby="emailHelp"
            placeholder="">
    </div>
    <div class="form-group">
        <label for="exampleInputPassword1">간단 코멘트</label>
        <input type="password" class="form-control" placeholder="">
    </div>
    <button type="submit" class="btn btn-primary">기사 저장</button>
</div>
```

* 크롬 콘솔창에서

```Javascript
$('#post-box').hide();
// id가 post-box인 것을 안보이게 한다. diplay : block -> none

$('#post-box').show();
// id가 post-box인 것을 보이게 한다. diplay : none -> block
```



### css값 가져오기

```Javascript
$('post-box').css('display');
// id가 post-box인 것의 css값을 가져온다.
```



### 태그 내 텍스트 입력하기

* input box

```Javascript
$('#post-url').val('텍스트 입력');
// .val()에 원하는 텍스트를 입력한다.
```

* 버튼의 텍스트

```Javascript
$('#btn-posting-box').text('포스팅 박스 닫기');
// id가 btn인 button의 텍스트를 변경할 수 있다.
```



### 태그 내 html 입력하기

* **div 태그에 id를 지정한다.**

```html
<div id="cards-box" class="card-columns"> <!-- id 지정 -->
    <div class="card">
      <img class="card-img-top" src="https://www.fodors.com/wp-content/uploads/2018/10/4_UltimateRome_PiazzaNavona-975x650.jpg" alt="Card image cap">
      <div class="card-body">
        <a href="https://naver.com/" class="card-title">여기 기사 제목이 들어가죠</a>
        <p class="card-text">여기에 기사 내용이 들어가겠죠</p>
        <p class="card-text comment">여기엔 코멘트가 들어갑니다</p>
      </div>
    </div>
  </div>
```

* 버튼 넣기

```Javascript
let temp_html = `<button>버튼입니다</button>`;
$('#cards-box').append(temp_html);
```

변수 **temp_html**에 텍스트로서 입력된 html코드가 저장된다. 그리고 **id**가  **cards-box**인 곳에 **.append**에 의해 추가된다.

여기서, html코드를 텍스트로 넣을 때 따옴표가 아닌, 반드시 **백틱(`)** 안에 넣어야 한다.



# 3. 자주 사용하는 Javascript

* **.includes('')** : 괄호안의 문자열이 있으면 **True**, 없으면 **False**를 **return.**
* **.empty()**: 내부 태그를 모두 비운다.



# Reference

**스파르타코딩 - 웹개발 종합반**