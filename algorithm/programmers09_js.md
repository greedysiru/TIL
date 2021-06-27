


# [프로그래머스] 약수의 합 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 약수의 합
function solution(n) {
  let answer = 0;
  // n의 각 약수를 구하고 answer에 누적하기
  for (let i = 1; i <= n; i++) {
    if (n % i === 0) {
      answer += i;
    }
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

