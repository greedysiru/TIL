# [프로그래머스]  n^2 배열 자르기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(n, left, right) {
    // n * n 만큼 길이를 가지는 1차원 배열을 초기화
    const array = [];
    const startRow = parseInt(left / n) + 1;
    const endRow = parseInt(right / n) + 1;
    const startCol = parseInt(left - ((startRow - 1) * n));
    const endCol = parseInt(right - ((startRow - 1) * n));


    console.log(startRow, endRow, startCol, endCol);
    for (let row = startRow; row <= endRow; row++) {
        for (let col = 1; col <= n; col++) {
           array.push(col < row? row : col);
        }
    }
    return array.slice(startCol, endCol + 1);
}

```



## Reference

[프로그래머스](https://programmers.co.kr)

