# [프로그래머스] N개의 최소공배수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// N개의 최소공배수
// 유클리드 호제법으로 최대공약수를 구하는 함수
function findGcd(a, b) {
  if (a % b === 0) {
    return b;
  } else {
    return findGcd(b, a % b);
  }
}

function solution(arr) {
  // 주어진 배열에 접근하여 최소공배수 구하기
  let a = arr[0];
  let b = 0;
  let lcm = 0;
  for (let i = 1; i < arr.length; i++) {
    b = arr[i];
    // 최소공배수
    lcm = (a * b / findGcd(a, b)) > lcm ? (a * b / findGcd(a, b)) : lcm;
    a = lcm;
  }
  return lcm;
}

```



## Comment

유클리드 호제법으로 최대공약수를 구하는 재귀함수를 선언하고, 주어진 배열에 접근하여 처음에는 0번, 1번 인덱스 요소의 최소 공배수를 구하고 그 이후에는 그 이전의 최소공배수와 배열의 요소의 최소공배수를 구해서 큰 최소 공배수로 최신화한다.



## Reference

[프로그래머스](https://programmers.co.kr)

