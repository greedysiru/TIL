# [생활코딩]WEB2-Node.js (6)(2020.12.19~)

**본 내용은 해당 [강의](https://opentutorials.org/course/3332) 토대로 작성**

## HTML-form

지금까지, 데이터 디렉토리에 접근할 수 있는 것은 자기 자신이기 때문에 컨텐츠 생성은 소유자만 할 수 있었다. 지금부터는, 사용자가 서버를 통해서 데이터를 전송하면 컨텐츠를 생성, 수정 삭제를 할 수 있도록 HTML-form을 알아본다.

인풋태그로 이제 서버에 데이터를 전송할 수 있다

텍스트에어리어는 여러줄 입력

서브밋은 서버에 전송하는 버튼생성

입력한 주소로 전송

각각 인풋(컨트롤)에 이름이 있어야함

```html
<form action="http://localhost:3000/process_create"> 
<p><input type="text" name="title"></p>
<p><textarea name="description"></textarea></p>
<p><input type="submit"></p>
</form>
```

`<form></form>` : HTML-form을 사용

​	-`action` : 각 각의 컨트롤`input, textarea`에 사용자가 입력한 정보를 `submit`했을 때 속성이 가르키는 곳으로 전송

`<input></input>` : 사용자가 데이터를 입력할 수 있는 컨트롤 생성

​	-`type="text"` : 텍스트 상자

​	-`type="submit"` : 제출버튼

`<textarea></textarea>` : 여러줄 입력할 수 있는 텍스트 상자

![Nodejs6-1](images/Nodejs6-1.png)

만들어진 컨트롤들에 위와 같이 입력하면 아래와 같은 URL이 만들어진다.(Not found 출력)

> http://localhost:3000/process_create?title=hi&description=greedy+siru

`form` 태그의 `action` 속성이 가르킨 주소로 각 컨트롤의 `name=입력 내용` 인 쿼리스트링이 생성된 것을 볼 수 있다. 하지만, 이것은 좋은 방식이 아니다. 왜냐하면 무분별하게 서버의 정보가 생성, 수정, 삭제가 될 수 있기 때문이다. 그러므로 HTML-form의 전송 방식을 다른 방법으로 해야한다.

```html
<form action="http://localhost:3000/process_create" method="post">
```

이렇게 `method="post"` 의 속성을 준다. 이렇게 하면, 아까와 똑같은 데이터를 입력해도 쿼리스트링이 생성되지 않는다.

> http://localhost:3000/process_create

그렇기 때문에, 일반적으로 사용자가 서버에서 데이터를 가져오는 경우에는 `method="get"` 속성을 부여하고(또는 생략) HTML-form처럼 사용자가 컨텐츠를 생성, 수정, 삭제하는 경우에는 `post` 를 사용한다.

