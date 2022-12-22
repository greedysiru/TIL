# 클린코드 자바스크립트 - 분기 다루기(삼항연산자 다루기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 삼항연산자

* 조건 처리를 짧게 할 수 있음
* 세 개의 피연산자를 취함
  * 조건? 참 : 거짓의 형태
  * 참과 거짓에는 식이 들어가야만 함
* 조건에 따라 참, 거짓 모두 필요할 때만 사용할 것

```JavaScript
// 조건? 참 : 거짓
isCat? '고양이' : '고양이 아님';
```



## 2. 과도한 삼항연산자 사용

* 과도하게 중첩하여 사용하면 가독성이 떨어짐
  * 조건부 처리가 많이 필요하면 switch-case 문으로 바꾸는 것이 나음
  * switch-case 문은 default로 엣지 케이스를 관리하기도 용이
* 괄호를 감싸 가독성을 높일 수도 있음



### switch-case 문으로 바꾸기

```JavaScript
// 중첩되어 가독성이 떨어짐
function getCatName() {
  return isSiru? 'siru' : isNuNu? 'nunu' : isMango? 'mango' : '몰라'
};
```



## 3. 삼항연산자 사용 예시

* 참, 거짓의 자리에 함수 호출을 넣을 수 있음
* nullable한 상황에서 유용하게 사용 가능

```JavaScript
const callCat = (isExistCat) => {
  const name = isExistCat? getCatName() : '없음';
  return `이리와 ${name}`;
}
```



* 단 void를 return 하는 함수를 호출하는 것은 if-else문을 권장

```JavaScript
const greeting = (isCat) => {
  // alert은 undefined를 return
  isCat
  	? alert('어서와 고양이')
  	: alert('오지마');
}
```



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)