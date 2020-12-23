# [생활코딩]WEB2-Node.js (8)(2020.12.23)



**상세 내용 [블로그](https://greedysiru.tistory.com/55?category=862259) 참고**



## App - 객체를 이용해서 템플릿 기능 정리 정돈하기

 `template` 접두어 함수를 객체로 정리한다.

```javascript
var template = {
   HTML:function(title, list, body, control){
     ...
   },List:function(filelist){
     ...	
     }
```

변수 `template` 을 선언하고 두 개의 함수를 넣어준다. 함수명을 지우고 key를 앞에 적어준다. 

객체화된 함수를 사용하는 것은 아래와 같다.

```javascript
template.HTML(){}
template.List(){}
```



## Node.js - 모듈의 형식

많은 객체를 모듈(Module)로 정리하여 파일 단위로 독립할 수 있다.

`mpart.js` 라는 파일의 객체를 외부에 사용할 수 있도록 맨 아래의 명령어를 입력

```javascript
var M = {
  v:'v',
  f:function(){
    console.log(this.v);
  }
}
module.exports = M;
```

`M` 이라는 객체를 모듈 바깥에서도 사용할 수 있도록 `exports`한다는 뜻이다.

별도의 파일 `muse.js`에서 아래와 같이 명령어를 입력한다

```javascript
var part = require('./mpart.js');
```

`require('./mpart.js')` 는 같은 디렉토리에 있는 `mpart.js`의 모듈을 가져온다.



## App 제작 - 모듈의 활용

 템플릿 기능을 모듈화 시킨다.

새로운 폴더 `lib`에 하위 파일 `template.js `를 생성한 뒤, 객체 `template` 를 복사 후 해당 파일에 붙여넣기 한다.

```javascript
module.exports = {
  HTML:function (title, list, body, control){
    ...
  }, List:function (filelist){
    ...
  }
}

```

`main.js` 에서 모듈을 가져오기 한다.

```javascript
...
var template = require('./lib/template.js');
...
```



# Reference

https://opentutorials.org/course/3332