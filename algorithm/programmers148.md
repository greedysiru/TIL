# [프로그래머스] 소인수분해 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (n) => {
    const answer = [];
    for (let i = 2; i <= n; i++) {
        if (n % i === 0) {
            let isPrime = true;
            for (let j = 2; j <= Math.sqrt(i); j++) {
                if (i % j === 0) {
                    isPrime = false;
                    break;
                }
            }
            if (isPrime === true) {
                answer.push(i);
                n /= i;
            }
        }
    }
    return [...new Set(answer)].sort((a, b) => a - b);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

