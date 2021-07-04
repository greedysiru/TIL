# [프로그래머스] 가장 큰 정사각형 찾기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 가장 큰 정사각형 찾기
function solution(board) {
  let answer = 0;
  if (board.length <= 1 || board[0].length <= 1) {
    return 1;
  }
  for (let i = 1; i < board.length; i++) {
    for (let j = 1; j < board[0].length; j++) {
      if (board[i][j] >= 1) {
        board[i][j] = Math.min(board[i - 1][j - 1], board[i - 1][j], board[i][j - 1]) + 1;
        answer = answer > board[i][j] ? answer : board[i][j];
      }
    }
  }
  return answer * answer;
}
```



## Comment

`이중 for문`으로 `board`를 접근한다. `i`가 행번호, `j`가 열번호일 때 `board[ i ] [ j ]`가 0보다 클때만 왼쪽, 대각선위, 위의 요소를 접근하여 그 중 최솟값 +1로 해당 요소에 입력한다. 그렇게 기록해 나갔을 때, 최댓값이 가장 큰 정사각형의 한 변이다.



## Reference

[프로그래머스](https://programmers.co.kr)

