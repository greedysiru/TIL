# [프로그래머스] 안전지대 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (board) => {
    const limit = board.length;
    const dx = [0, 0, 1, 0, -1, 1, 1, -1, -1];
    const dy = [0, 1, 0, -1, 0, -1, 1, 1, -1];
    const visited = [];
    for (let i = 0; i < limit; i++) {
        for (let j = 0; j < limit; j++){
            if (board[i][j] === 1  && !visited.includes(`${j},${i}`)) {
                for (let k = 0; k < 9; k++) {
                    const nextX = j + dx[k];
                    const nextY = i + dy[k];
                    if (0 <= nextX && nextX < limit && 0 <= nextY && nextY < limit && board[nextY][nextX] !== 1) {
                        board[nextY][nextX] = 1;
                        visited.push(`${nextX},${nextY}`);
                    }
                }
            }
        }
    }
    let answer = 0;
    board.forEach((row) => row.forEach((area) => {
        if (area === 0) {
            answer += 1;
        }
    }))
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

