# 클린코드 자바스크립트 - 함수 다루기(argument & parameter)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## argument & parameter

### parameter

* 매개변수
* 함수를 선언할 때 함수로 들어올 변수에 대한 명칭
  * argument가 들어왔을 때 parameter는 초기화 됨(호출 시점)
* Foraml Parameter라고도 함
  * 격식을 갖춘, 형식을 갖춘
  * 호출하는 측으로 하여금 어떤 것을 넘기고 어떻게 사용될 것인지 알 수 있어야 한다는 의미

```JavaScript
function example(parameter) {
  console.log(parameter);
}
```



### argument

* 인자, 인수
* 함수를 호출할 때 넘기는 변수
  * 함수에서 사용될 실질적인 값
* Actual Parameter
  * 실제로 사용되는

```JavaScript
const argument = 'example argument';
example(argument);
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

