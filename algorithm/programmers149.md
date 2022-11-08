# [프로그래머스] 구슬을 나누는 경우의 수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const factorial = (n) => {
    if (n <= 1) {
        return BigInt(1);
    } else {
        return BigInt(n) * factorial(BigInt(n) - BigInt(1));
    }
}

const solution = (balls, share) => factorial(balls) / (factorial(balls - share) * factorial(share));
```



## Reference

[프로그래머스](https://programmers.co.kr)

