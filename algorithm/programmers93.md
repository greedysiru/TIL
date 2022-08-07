# [프로그래머스] 크레인 인형뽑기 게임 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
// 행, 열변환 함수
const transpose = matrix => matrix.reduce((prev, rows) => rows.map((row, index) => [...(prev[index] || []), rows[index]]), []);

function solution(board, moves) {
    let answer = 0;
    // 주어진 board 배열의 행, 열을 바꿈
    // 0을 제거
    // 뒤집기
    const convertedBoard = transpose(board).map(rows => rows.filter(item => item !== 0).reverse());
    // 주어진 moves대로 바구니에 인형을 옮겼을 때 터트려져 사라진 인형 구하기
    const basket = [];
    moves.forEach((move) => {
        const item = convertedBoard[move - 1].pop();
        if (item && basket[basket.length - 1] === item) {
            basket.pop();
            answer += 2;
        } else {
         basket.push(item);   
        }
    })
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

