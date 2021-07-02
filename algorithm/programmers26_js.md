# [프로그래머스] 자연수 뒤집어 배열로 만들기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 자연수 뒤집어 배열로 만들기
function solution(n) {
  let answer = [];
  const nString = String(n);
  for (let i = nString.length - 1; i >= 0; i--) {
    answer.push(parseInt(nString[i]));
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

