# [프로그래머스] 콜라 문제 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (a, b, n) => {
    let answer = 0;
    while (n >= a) {
        const cola = Math.floor(n / a) * b;
        const rest = n % a;
        n = rest + cola;
        answer += cola;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

