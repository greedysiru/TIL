# 클린코드 자바스크립트 - 분기 다루기(else if & else 피하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. else if 피하기

* else if는
  * else의 블록 안에서 새로운 if문을 실행하는 것과 같음
* else if를 줄이는 것이 권장됨
  * switch case 문으로 바꾸기
  * 또는 명확하게 조건을 분리
* else if는 파이프라인처럼 흐르는 것이 아님을 명심

```JavaScript
const x = 1;

if (x >= 0) {
  'x는 0과 같거나 크다'; // 여기서 실행되고
} else if (x > 0) {
  'x는 0보다 크다';
} else {
  'Else';
}

// 위 조건문과 아래는 동일하게 실행 됨
if (x >= 0) {
  'x는 0과 같거나 크다';
} else {
  if (x > 0) {
    'x는 0보다 크다';
  }
}
```



## 2. else 피하기

* 단축평가로 줄일 수 있음
* if - else를 함수안에 쓰면
  * 참과 거짓일 때의 반환이 명백하게 return
  * 하나의 함수가 두가지 역할을 하게 될 수 있음

```JavaScript
// user age가 성인일 때만 특수 함수 실행
// 하나의 함수가 두 개의 역할을 하게 됨
const goToMainPageForAdultUser = (user) => {
  const {age} = user;
  
  if (age < 20) {
    return '미성년자 입니다.';
  } else {
    goToMainPage();
  }
}

// 아래처럼 리팩터링할 수 있음(else 피하기)
const goToMainPageForAdultUser = (user) => {
  const {age} = user;
  
  if (age >= 20) {
    goToMainPage();
  }
  
  return '미성년자 입니다.';
}
```







## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

