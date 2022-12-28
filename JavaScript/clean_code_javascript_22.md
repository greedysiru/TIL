# 클린코드 자바스크립트 - 분기 다루기(Default Case 고려하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Default Case 고려하기

* 프로그래밍에서 Default Case(또는 Edge Case)를 고려하는 것은 매우 중요 함
* 안정성 높고 확장성 높은 코드를 만들 수 있음
* 어떠한 라이브러리던 Default Case가 고려되어 있음



### 함수의 예시

* 함수를 호출했을 때 매개변수를 전달하지 않은 케이스에서의 동작을 고려해야함
  * 인자 기본값 정의

```JavaScript
const callMyCat = (catName = '고양아') => {
	console.log(`${catName} 이리와`);
}

// 또는 아래처럼 표현할 수 있음
function callMyCat(catName) {
  catName = catName || '고양아';
	console.log(`${catName} 이리와`);
}
```



### switch-case 문의 예시

* switch-case 문에서의 분기처리에서 예기치 못한 입력값으로 인해 문제가 발생할 수 있음
  * 정해진 방식이 아닌 입력값이 들어오면, 에러 처리를 하기

```JavaScript
// 사용자가 입력한 userInputDay를 분기처리하는 함수
const registerDay(userInputDay) {
  // case문에서 고려되지 않은 userInputDay가 입력되면 에러가 발생 할 수 있음
  switch (userInputDay) {
    case '월요일': // some code
    case '화요일': // some code
    case '수요일': // some code
    case '목요일': // some code
    case '금요일': // some code
    case '토요일': // some code
    case '일요일': // some code
    default:
      // 명시적으로 에러를 throw
      throw Error('입력값이 올바른 형식이 아닙니다.');
  }
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

