

# [프로그래머스] 숫자 짝궁 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
function solution(X, Y) {
    let pairNum = [];
    const numberRecord = {
        0: 0,
        1: 0,
        2: 0,
        3: 0,
        4: 0,
        5: 0,
        6: 0,
        7: 0,
        8: 0,
        9: 0,
    };
    for (const xNum of X) {
        numberRecord[xNum] += 1;
    }
    
    for (const yNum of Y) {
        if (numberRecord[yNum] !== 0) {
            pairNum.push(yNum);
            numberRecord[yNum] -= 1;
        }
    }
    const answer = pairNum.length > 0? pairNum.sort((a, b) => b - a).join('') : '-1';
    return answer[0] === '0'? '0': answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

