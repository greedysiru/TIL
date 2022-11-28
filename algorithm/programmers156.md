# [프로그래머스] 평행 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
function solution(dots) {
    const slopes = [];
    let answer = 0;
    for (let i = 0; i < dots.length; i++) {
        const currentDot = dots[i];
        const [x1, y1] = currentDot;
        for (let j = i + 1; j < dots.length; j++) {
            const nextDot = dots[j];
            const [x2, y2] = nextDot;
            const slope = Math.abs(x1 - x2) / Math.abs(y1 - y2);
            if (slopes.includes(slope)) {
                answer = 1;
            }
            slopes.push(slope);
        }
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

