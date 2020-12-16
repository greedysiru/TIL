 # [생활코딩]Node.js (3)(2020.12.14)



**상세 내용 [블로그](https://greedysiru.tistory.com/28) 참고**



## 동적인 웹 페이지 만들기 -1

쿼리스트링에 따라서 웹 페이지의 title과 본문 제목을 바꾸는 기능을 추가.

```javascript
<title>WEB1 - ${queryData.id}</title>
<h2>${queryData.id}</title>
```

리스트의 하이퍼링크를 아래처럼 변경하여, 쿼리스트링에 해당 id 입력하는 기능을 추가.

```javascript
<ol>
    <li><a href="/?id=HTML">HTML</a></li>
    <li><a href="/?id=CSS">CSS</a></li>
    <li><a href="/?id=JavaScript">JavaScript</a></li>
</ol>
```



## 파일 읽기

확장자가 .js인 파일을 추가하고 아래의 명령어를 입력하면 Node.js의 File system 모듈로 다른 파일을 읽을 수 있다.

```javascript
var fs = require('fs');
fs.readFile('sample.txt','utf-8', function(err,data){
  	console.log(data)
});
```

위 명령어는 sample.txt의 data를 콘솔창에 출력해준다.



## 동적인 웹 페이지 만들기 -2

 Node.js의 File system 모듈로 웹 페이지의 쿼리스트링에 따라서 해당하는 텍스트들을 불러오게 할 수 있다. 설명은 명령어의 주석 참고.

```javascript
var http = require('http');
var fs = require('fs'); //File system 모듈을 사용한다는 변수
var url = require('url');

var app = http.createServer(function(request,response){
    var _url = request.url;
    var queryData = url.parse(_url, true).query;
    var title = queryData.id;
    console.log(queryData.id);
    if(_url == '/'){
      title = 'welcome' ;
    }
    if(_url == '/favicon.ico'){
      return response.writeHead(404);
    }
    response.writeHead(200);
    fs.readFile(`data/${queryData.id}` , 'utf8', function(err, description){ // 쿼리스트링과 같은 파일명을 찾는다.
      var template = ` // 해당 파일에서 가져온 텍스트는 description이라는 함수로 정의
      <!doctype html>
      <html>
      <head>
        <title>WEB1 - ${title}</title>
        <meta charset="utf-8">
      </head>
      <body>
        <h1><a href="/">WEB</a></h1>
        <ul>
          <li><a href="/?id=HTML">HTML</a></li>
          <li><a href="/?id=CSS">CSS</a></li>
          <li><a href="/?id=JavaScript">JavaScript</a></li>
        </ul>
        <h2>${title}</h2>
        <p>${description}</p> // description을 출력
      </body>
      </html>
      `;
      response.end(template); // 사용자에게 template을 출력
    })


});
app.listen(3000);


```



# Reference

https://opentutorials.org/course/3332

