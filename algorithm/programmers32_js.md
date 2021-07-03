# [프로그래머스] 평균 구하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 평균 구하기
function solution(arr) {
  // arr의 모든 합
  const arrSum = arr.reduce((prev, curr) => prev + curr);
  // 평균
  const answer = arrSum / arr.length;
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

