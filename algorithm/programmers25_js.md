# [프로그래머스] 자릿수 더하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 자릿수 더하기
function solution(n) {
  let answer = 0;
  const nString = String(n);
  for (let i = 0; i < nString.length; i++) {
    answer += parseInt(nString[i]);
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

