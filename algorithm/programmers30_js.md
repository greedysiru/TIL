# [프로그래머스] 짝수와 홀수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 짝수와 홀수
function solution(num) {
  let answer = '';
  if (num % 2 === 0) {
    answer = 'Even';
  } else {
    answer = 'Odd';
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

