# 타입스크립트 입문 - 함수 타입 정의하기

**본 내용은 인프런 장기효(캡틴판교)님의 타입스크립트 입문 - 기초부터 실전까지 강의를 토대로 작성하였습니다.**



## 1. 파라미터, 반환값

### 함수의 파라미터에 타입을 정의

```TypeScript
// 이 함수는 두 개의 숫자를 받음
function sum(a: number, b: number) {
  return a + b;
}

sum(10, 20);

sum(10, '20'); // 에러 발생
```



### 함수의 반환 값에 타입을 정의

```TypeScript
// 이 함수는 숫자를 리턴
function isNumber(): number {
  return 10;
}

isNumber(); // 10
```



### 두 방식을 함께 사용

* 함수의 반환 값에 타입을 정하지 않을 때는 void라도 사용 할 것

```TypeScript
function sum(a: number, b: number): number {
  return a + b;
}

sum(10, 20); // 30

sum(10, '20'); // 에러 발생
```



## 2. 파라미터를 제한하는 특성

* 타입스크립트에서는 함수의 인자를 모두 필수 값으로 간주
  * 함수의 매개변수를 설정한 이상 undefined, null 이라도 인자로 넘겨야 함
* 정의된 매개변수 만큼의 값만 인자로 받을 수 있고 추가로 인자를 받을 수 없음
* 함수를 엄격하게 체크하여 오류 방지
* 자바스크립트는 정의된 매개변수 갯수 만큼 인자를 넘기지 않아도 됨(매개변수의 생략 또는 추가가 가능)

```TypeScript
function sum(a: number, b: number, c: number): number {
  return a + b + c;
}

sum(10, 20); // error
sum(10, 20, 30); // 60
```



## 3. 옵셔널 파라미터

* 선택적 파라미터
* 타입 선언시 필수가 아닌 매개변수는 ?을 이용해서 생략 가능하도록 할 수 있음

```TypeScript
// c 매개변수는 생략 가능
function sum(a: number, b: number, c?: number): number {
  return a + b + c;
}

sum(10, 20); // 30
sum(10, 20, 30); // 60
```


# Reference

[타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/타입스크립트-입문)

[타입스크립트 핸드북](https://joshua1988.github.io/ts/intro.html)