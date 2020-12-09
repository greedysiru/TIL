# [생활코딩]WEB2-JavaScript (4) (2020.12.8)

**상세 내용 [블로그](https://greedysiru.tistory.com/19) 참조**

## Function(함수)

많은 코드를 함수를 정의해서 사용할 수 있다.



## 함수 문법

```JavaScript
function 함수명( ){
  
}
```



## Parameter(매개변수)와 argument(인자)

함수에 매개변수를 적용할 수 있다. 전달 되는 값은 인자라고 한다.

```javascript
<script>
	fucntion sum(left,right){
    document.write(left+right+'<br>');
    }
    sum(2,3) /// 5
    sum(3,4) /// 7
</script>
```



## Return

함수가 실행되어 값이 출력되었을 때 입력된 것을 표현식이라고 한다.함수에서 표현식을 다시 출력해서 원자화된 기능을 다양한 맥락에서 활용할 수 있다.



## 리팩토리

night/day 토글 버튼의 기능을 함수로 정의해서 사용할 수 있다.

```javascript
<head>
<script>

    function nightDayHandler(self){
      var target = document.querySelector('body')
        if(self.value === 'night'){
          target.style.backgroundColor = 'black';
          document.querySelector('body').style.color = 'white';self.value='day';

          var alist = document.querySelectorAll('a');
          var i = 0 ;
          while(i < alist.length){
          console.log(alist[i]);
          alist[i].style.color = 'powderblue'
          i = i + 1;
            }}
          else{
          target.style.backgroundColor = 'white';
          target.style.color = 'black';
          self.value='night';
          var alist = document.querySelectorAll('a');
          var i = 0 ;
          while(i < alist.length){
          console.log(alist[i]);
          alist[i].style.color = 'blue'
          i = i + 1;
            }}}
</script>
</head>

<input type="button" value="night" onclick="nightDayHandler(this);">
```

this를 self로 바꾼다. this는 이벤트가 소속되어 있는 태그를 가르키지만, 함수로 정의 되면 다른 것을 가르키게 되기 때문이다.



# Reference

https://opentutorials.org/course/3085