# [생활코딩]WEB2-Node.js (10)(2020.12.24)



**상세 내용 [블로그](https://greedysiru.tistory.com/58) 참고**



## API

프로그래밍 하기 위해서 제공되는 Interface를 `API(Application Programming Interface)`라고 한다. `API`는 프로그래밍 언어를 다룰떄의 조작장치 같은 것이다.

기존 코드에 사용한 `API`는 아래와 같다.

```javascript
var http = require('http');
...
var app = http.createServer(function(request,response){
...
}
```

`createServer` : 웹 서버를 만들고 외부에서 요청이 들어오면 콜백함수를 실행한다. 리턴 값으로 `http.server` 를 가진다.

`request` : 웹 브라우저로부터 들어온 요청에 대한 여러가지 정보를 담고 있는 객체이다. 

 `response` : 전송하고 싶은 정보를 응답할 수 있도록 한다.

```javascript
app.listen(3000);
```

리턴 값을 적용하면 `server.listen` 이다. 이것은 요청에 대해서 응답할 수 있도록  http 서버를 구동시킨다. 입력된 숫자는 `port`를 의미한다. 해당 포트로 들어오면 애플리케이션이 동작한다.



## 보충수업 - PM2 사용법

```
pm2 kill
```

pm2 실행 앱 전부 종료

```
pm2 main.js --watch --no-daemon
```

 백그라운드로 실행하지 않는다. 동시에 로그도 볼 수 있다.(daemon: 백그라운드 실행 프로그램)

```
pm2 start main.js --``watch` `--ignore-``watch``=``"data/* sessions/*"`  `--no-daemon
```

특정 디렉토리에 대한 `watch` 를 하지 않음



# Reference

https://opentutorials.org/course/3332