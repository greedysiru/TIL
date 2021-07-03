# [프로그래머스] 하샤드 수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 하샤드 수
function solution(x) {
  // 자릿수의 합을 구하기위해 문자열 화
  const xString = String(x)
  // 자릿수의 합 구하기
  let xSum = 0;
  for (let xStr of xString) {
    xSum += parseInt(xStr);
  }
  // 하샤드 수인지 검사
  if (x % xSum === 0) {
    return true;
  } else {
    return false;
  }
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

