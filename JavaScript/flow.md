# 기초 JS, CS 상식 - 흐름 제어



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 1. 흐름 제어

* Control Flow
  * 흐름을 제어하는 방법 중 하나
  * 조건, 반복을 통해 상태를 제어
  * if, for 등의 방법 이용
* Data Flow
  * 함수형 프로그래밍 방식



### Control Flow vs. Data Flow

| Cotrol Flow      | Data Flow |
| ---------------- | --------- |
| Goto             | Stateless |
| If / Then / Else | Recursion |
| Switch / Case    | Pipe      |
| For / While      |           |



## 2. 조건문

* Control Flow에서 사용
* 조건이 맞을 때만 실행되는 문장(Statements) 문법
* Yes or No



### if

* 괄호 안 조건식이 참인 경우 실행
* else if, else도 같이 사용 가능
* **JavaScript의 암묵적 타입변환으로 boolean이 아닌 데이터 형식이라도 true, false 취급될 수 있음에 주의**
  * ex) falsy(undefined, null, 0, NaN, "")

```JavaScript
const age = 30;

if (age > 20) {
  console.log('성인입니다.');
}	 else if (age < 20) {
  console.log('미성년자입니다.');
}
```





### switch

* 괄호 안 값에 따라 분기되는 문법
* case, default와 함께 쓰임
* **case마다 명시적으로 break를 적어야 다음 case로 넘어가지 않음**

```JavaScript
const siru = 'cat';
switch (score) {
  case 'cat':
    console.log('It is cat');
    break;
  case 'dog':
    console.log('It is dog');
    break;
  default:
    console.log('모르겠어');
}
```





## 3. 반복문

* 반복적인 작업을 지시



### for

* 가장 기초적인 반복문
* 초기문, 조건문, 증감문으로 이루어짐
* 조건문의 결과가 거짓이면 반복 종료

```JavaScript
for (let i = 0; i <= 10; i++) {
  console.log(i);
}
```



### while

* 괄호안 조건이 거짓이 될 때까지 반복

```JavaScript
let start = 0;
while (start <= 10) {
  console.log(`${start}입니다.`);
  start += 1;
}
```



### do - while

* do 블록 안의 로직을 진행 후 while 안의 조건 검사

```JavaScript
let start = 11;
do {
  console.log(`${start}입니다.`);
} while (start <= 10);
```





## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

