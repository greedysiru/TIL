# [생활코딩]WEB2-Node.js (1)(2020.12.11)



**상세 내용 [블로그](https://greedysiru.tistory.com/21) 참고**



## Node.js

2008년에 구글 v8엔진 기반으로 JavaScript를 사용하는 런타임 환경.



## 설치

[nodejs.org/en/](https://nodejs.org/en/) 에서 LTS버전 설치. 이후 터미널에서

``` javascript
node -v
```

버전확인이 되면 정상 설치 완료.



## 서버구축

``` javascript
var http = require('http');
var fs = require('fs');
var app = http.createServer(function(request,response){
    var url = request.url;
    if(request.url == '/'){
      url = '/index.html';
    }
    if(request.url == '/favicon.ico'){
      response.writeHead(404);
      response.end();
      return;
    }
    response.writeHead(200);
    response.end(fs.readFileSync(__dirname + url));

});
app.listen(3000);
```

입력 후, 터미널에서

```javascript
node main.js
```

실행하면 서버가 구축된다. 웹 브라우저에서 locallhost:3000으로 들어가서 확인. 



## 명령어 정리

`node -v` : 노드 버전 확인

`console.log( )` : 코드 실행 후 출력

`.exit` : node 나가기

`response.end(  )` : 웹 페이지에서 데이터 전송



# Reference

https://opentutorials.org/course/3332