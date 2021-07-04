# [프로그래머스] 행렬의 곱셈 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 행렬의 곱셈
function solution(A, B) {
  let answer = [];

  for (let i = 0; i < A.length; i++) {
    // 행렬 A의 행 접근 - A
    const row = A[i];
    answer.push([]);
    // 행렬 B의 열 접근해서 곱하기 - B
    // 행렬 B의 열 길이
    for (let j = 0; j < B[0].length; j++) {
      let sum = 0;
      // 행렬 B의 행 길이
      // B는 열을 고정해놓고 행을 이동하기 - C
      for (let k = 0; k < B.length; k++) {
        sum += row[k] * B[k][j];
      }
      answer[i].push(sum);
    }
  }
  return answer;
}
```



## Comment

행렬의 곱셉은 앞의 행렬의 행꽈 뒤의 행렬의 열끼리 곱한다. 3중 `for문`을 사용하여, 

1. 앞의 행렬의 행을 고정시키고 - A
2. 뒤의 행렬의 열을 고정시켜  - B
3. 각각 자리에 맞는 요소끼리 곱한 후 더해준다. - C



## Reference

[프로그래머스](https://programmers.co.kr)

