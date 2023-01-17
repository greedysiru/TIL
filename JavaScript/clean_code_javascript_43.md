# 클린코드 자바스크립트 - 함수 다루기(함수, 메서드, 생성자)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 함수, 메서드, 생성자

### 함수

* JavaScript 함수는 1급 객체
  * 변수, 데이터에 담길 수 있음
  * 매개변수로 전달 가능(call back)
  * 함수가 함수를 반환(고차 함수)
  * 고차 함수, curring, 함수형 프로그래밍 가능

```JavaScript
function func() {
  ...
}
```



### 메서드

* 객체에 의존성이 있는 함수
* OOP 관점에서 행동을 의미

```JavaScript
const cat = {
  nyam() {
    console.log('냠냠');
  }
}

cat.nyam();
```



### 생성자 함수

* 인스턴스를 생성하는 역할
* Class문법은 생성자 함수의 문법적 설탕

```JavaScript
function Func() {
  return this;
}

const instance = new Func();
```



### this

* 함수, 메서드,  생성자의 this는 각각 다름

|        | this               |
| ------ | ------------------ |
| 함수   | 전역(global)       |
| 메서드 | 메서드가 속한 객체 |
| 생성자 | 생성될 인스턴스    |



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

