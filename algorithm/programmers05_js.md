


# [프로그래머스] 수박수박수박수박수박수? - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 수박수박수박수박수박수?
function solution(n) {
  let answer = '';
  for (let i = 1; i <= n; i++) {
    if (i % 2 === 1) {
      answer += '수'
    }
    else if (i % 2 === 0) {
      answer += '박'
    }
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

