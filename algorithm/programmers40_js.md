# [프로그래머스] 피보나치 수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 피보나치 수
// 피보나치 수를 메모이제이션
const fiboMemo = {
  0: 0,
  1: 1,
  2: 1,
}
function solution(n) {
  if (fiboMemo[n]) {
    return fiboMemo[n];
  } else {
    // 해당수까지 메모이제이션을 참고하며 답 구하기
    for (let i = 3; i <= n; i++) {
      fiboMemo[i] = (fiboMemo[i - 2] + fiboMemo[i - 1]) % 1234567;
    }
  }
  return fiboMemo[n];
}

```



## Comment

DP로, 피보나치 수열을 구한다. 메모이제이션한 값이 있으면 해당 값을 바로 `retrun`하고  그렇지 않으면 피보나치 수열의 점화식을 `for문`안에서 기록해나가며 목표로한 지점까지의 피보나치 수를 구한다.



## Reference

[프로그래머스](https://programmers.co.kr)

