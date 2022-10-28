# [프로그래머스]  캐릭터의 좌표 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
function solution(keyinput, board) {
    var answer = [];
    const widthLimit = Math.abs((board[0] - 1) / 2);
    const heightLimit = Math.abs(board[1] - 1) / 2;
    const vector = [{left: -1, right: 1}, {up: 1, down: -1}];
    return keyinput.reduce((position, cur) => {
        return position.map((p, index) => {
            const move = vector[index][cur];
            if (move !== undefined) {
                const acc = p + move;
                if (index === 0 && Math.abs(acc) <= widthLimit) {
                    return acc;
                } else if (index === 1 && Math.abs(acc) <= heightLimit) {
                    return acc;
                }
            }
            return p;
        });
    }, [0, 0]);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

