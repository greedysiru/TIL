# 함수형 프로그래밍과 ES6+ - 함수형 자바스크립트 기본기



**본 내용은 프로그래머스의 함수형 프로그래밍과 ES6+ 강의를 토대로 작성하였습니다.**



## 1. 평가

* 코드가 계산(Evaluation)되어 값을 만드는 것

```JavaScript
1 + 2 // 3
[1, 1 + 2] // [1, 3]
['siru', ...['nunu', 'mango']] // ['siru', 'nunu', 'mango']
```



## 2. 일급

* 값으로 다룰 수 있음
* 변수에 담을 수 있음
* 함수의 인자로 사용 될 수 있음
* 함수의 결과로 사용될 수 있음



## 3. 일급 함수

* 함수를 값으로 다룰 수 있음
* 조합성과 추상화의 도구
  * 함수형 프로그래밍의 핵심
* 함수는 함수를 return할 수 있음

```JavaScript
const addFunc = (num1, num2) => num1 + num2;
const totalSum = addFunc(2, 3) + addFunc(5, 10); // 20

// 함수 안에서 함수가 Return
const foo = () => () => 'innter function return';
console.log(foo()); // () => 'inner function return'
console.log(foo()()); // inner function return
```



## 4. 고차 함수

* 함수를 값으로 다루는 함수
  * 함수를 인자로 받아 실행하는 함수
  * 함수를 만들어 return하는 함수



### 함수를 인자로 받아 실행하는 함수

```JavaScript
const apply1 = f => f(1);
const add2 = a => a + 2;
// apply1 함수는 add2함수를 인자로 전달 받음
// 전달받은 add2함수에 1을 인자로 전달하여 실행한 값을 return
console.log(apply1(add2)); // 3
```



```JavaScript
const times = (f, n) => {
  // n만큼 f를 실행하는 함수
  let i = -1;
  while (++i < n) f(i);
} 

times(console.log, 3); // 0 1 2
```



### 함수를 만들어 리턴하는 함수

* 클로저를 만들어 리턴하는 함수

```JavaScript
const addMaker = a => b => a + b;

// 클로저
// add10은 a가 10인 것을 기억하고 있음
const add10 = addMaker(10);
console.log(add10(5)); // 15;
```



## Reference

[[프로그래머스] 함수형 프로그래밍과 ES6+](https://school.programmers.co.kr/learn/courses/7637)

