# [프로그래머스] 과일 장수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (k, m, score) => {
    let profit = 0;
    // 1. score 내림차순 정렬
    score.sort((a, b) => b - a);
    // 2. 상자만들기
    let startIndex = 0;
    let endIndex = m;
    while (endIndex <= score.length) {
        const box = score.slice(startIndex, endIndex);
        startIndex += m;
        endIndex += m;
        profit += Math.min(...box) * m;
    }
    return profit;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

