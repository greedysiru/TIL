# [프로그래머스] x만큼 간격이 잇는 n개의 숫자 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// x만큼 간격이 잇는 n개의 숫자
function solution(x, n) {
  let answer = [];
  let number = x;
  for (let i = 0; i < n; i++) {
    answer.push(number)
    number += x;
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

