# 함수형 프로그래밍과 ES6+ - 제너레이터와 이터레이터



**본 내용은 프로그래머스의 함수형 프로그래밍과 ES6+ 강의를 토대로 작성하였습니다.**



## 제너레이터

* 이터레이터이자 이터러블을 생성하는 함수
* well-formed iterator를 반환하는 함수
* 제너레이터로 생성된 이터러블은 이터러블/이터레이터 프로토콜을 만족하므로 `for...of`, 전개 연산자, 구조 분해, 나머지 연산자를 사용할 수 있음



### 제너레이터 함수 정의

* 함수 선언식에 별표를 붙여 정의
* `yield` 를 통해 몇 번의 `next` 를 통해 값을 반환할 지 정할 수 있음
* 제너레이터 함수가 `return` 하는 값은 `done`이 `true`일 때 반환하는 값
  * `for...of`의 마지막 순회에선 반환하지 않는 값임에 주의(done이 false 일때만 순회하므로)

* 순회할 값을 문장으로 표현
* `if`문을 사용하여 조건부로 순회할 수 있도록 함
* **어떠한 상태나 값이든 순회할 수 있도록 만듦**

```JavaScript
function *gen() {
  yield 1;
  yield 2;
  yield 3;
  // 생성된 이터레이터가 순회를 마치고 done이 true일 때 반환하는 값
  return 999;
}
// 이터레이터를 반환
const iter = gen();
// 이터레이터이므로 next메서드로 순회 가능
console.log(iter.next()); // 1
...
```



## Reference

[[프로그래머스] 함수형 프로그래밍과 ES6+](https://school.programmers.co.kr/learn/courses/7637)

