# [프로그래머스]  멀리 뛰기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
// 메모이제이션
// 칸수에 따른 해
// n번째 해 = (n - 1번째 해) + (n -2번째 해)
const memo = [0, 1, 2, 3, 5];


function solution(n) {
    if (memo[n]) return memo[n];
    for (let i = 5; i <= n; i++) {
        memo[i] = (memo[i - 1] + memo[i - 2]) % 1234567;
    }
    return memo[n];
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

