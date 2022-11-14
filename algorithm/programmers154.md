# [프로그래머스] 유한소수 판별하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const getGCD = (a, b) => {
     if (a % b === 0) {
        return b
    } else {
        return getGCD(b, a % b);
    }
}

const isPrime = (num) => {
    for (let i = 2; i < num; i++) {
        if (num % i === 0) {
            return false;
        }
    }
    return true;
}

const solution = (a, b) => {
    const aAndBGCD = getGCD(a, b);
    const reducedA = a / aAndBGCD;
    const reducedB = b / aAndBGCD;
    const divisors = [];
    for (let j = 2; j <= reducedB; j++) {
        if (isPrime(j) && reducedB % j === 0) {
            divisors.push(j);
        }
    }
    return  divisors.filter(divisor => divisor !== 2 && divisor !== 5).length === 0? 1 : 2;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

