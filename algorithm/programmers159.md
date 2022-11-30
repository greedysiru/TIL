# [프로그래머스] 삼각형의 완성 조건 (2) - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
function solution(sides) {
    let answer = 0;
    const lagerSide = Math.max(...sides);
    const smallerSide = Math.min(...sides);
    for (let otherSide = lagerSide - smallerSide + 1; otherSide <= lagerSide; otherSide++) {
        answer += 1;
    }
    for (let otherSide = lagerSide + 1; otherSide < lagerSide + smallerSide; otherSide++) {
        answer += 1;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

