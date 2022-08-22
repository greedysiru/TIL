# [프로그래머스]  2 x n 타일링 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
const memo = {
    1: 1,
    2: 2,
    3: 3,
    4: 5,
}

function solution(n) {
    if (memo[n]) {
        return memo[n];
    }
    for (let i = 5; i <= n; i++) {
        memo[i] = (memo[i - 2] + memo[i - 1]) % 1000000007;
    }
    return memo[n];
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

