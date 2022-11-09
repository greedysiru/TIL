# [프로그래머스] 직사각형 넓이 구하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (dots) => {
    const parsedDots = dots.reduce((acc, cur) => {
        acc[0] = [...new Set([...acc[0], cur[0]])];
        acc[1] = [...new Set([...acc[1], cur[1]])];
        return acc;
    }, [[],[]]);
    const [x1, x2] = parsedDots[0];
    const [y1, y2] = parsedDots[1];
    const width = Math.abs(x1 - x2);
    const height = Math.abs(y1 - y2);
    return width * height;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

