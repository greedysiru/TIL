# 함수형 프로그래밍과 ES6+ - 사용자 정의 이터러블, 이터러블/이터레이터 프로토콜 정의/전개연산자



**본 내용은 프로그래머스의 함수형 프로그래밍과 ES6+ 강의를 토대로 작성하였습니다.**



## 사용자 정의 이터러블

```JavaScript
const iterable = {
  // 이터러블은 Symbol.iterator를 구현해야 함
  // 이 예시는 3 ~ 1까지 순회하도록 함
  [Symbol.iterator]() {
    // 초기값(클로저)
    let i = 3;
    // iterator를 반환해야 함
    return {
      	// iterator는 next 메서드를 가짐
      	next() {
          // next 메서드는 value와 done을 반환
          // value: 3 -> 2-> 1로 반환하게 됨
          // i가 0이면, 순회를 다 한것으로 done이 true
          return i === 0? {done: true} {value: i--, done: false};
        },
      	// 자기 자신을 반환(well formed iterator)
      	[Symbol.iterator]() { return this };
    }
  }
};
// 이터러블이므로 순회 가능
for (const j of iterable) console.log(j);

const arr = [1, 2, 3];
let iter = arr[Symbol.iterator]();
// iter 이터레이터 역시 Symbol.iterator를 가짐
// 호출 시, 자기 자신을 반환함
console.log(iter[Symbol.iter] === iter); // true
```



### well formed iterator

* 모든 요소를 순회할 수 있고
* 중간에 멈출 수 있으며
* 멈춘 곳 다음부터 순회할 수 있어야 함
* Symbol.iterator를 가짐
  * 호출 시, 자기 자신을 반환
* **이전까지 진행되어 있던 자기 자신을 반환하여 계속해서 next 메서드를 호출 할 수 있도록 해야 함** 
  * 이 조건을 만족하지 않으면, 이터러블이 아님



## 이터러블/이터레이터 프로토콜 정의

* **순회가 가능한 형태의 값이면 이 프로토콜을 준수해야 함**
  * NodeList
* Symbol.iterator가 구현되어 있어야 함
  * 호출 시 iterator를 반환
* iterator는
  * next 메서드를 반환
    * value, done을 반환
  * 해당 순회의 자신을 반환하는 Symbol.iterator를 반환

## 전개연산자

* 전개연산자를 사용하려면 이터러블 프로토콜을 만족해야 함

## Reference

[[프로그래머스] 함수형 프로그래밍과 ES6+](https://school.programmers.co.kr/learn/courses/7637)

