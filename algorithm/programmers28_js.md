# [프로그래머스] 정수 제곱근 판별 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 정수 제곱근 판별
function solution(n) {
  let answer = -1;
  // n의 제곱근 구하기
  const nSqrt = Math.sqrt(n);
  // 정수인지 판별
  if (Number.isInteger(nSqrt)) {
    answer = (nSqrt + 1) ** 2;
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

