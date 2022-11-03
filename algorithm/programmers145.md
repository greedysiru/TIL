# [프로그래머스] 분수의 덧셈 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
// 유클리드 호제법으로 최대공약수 구하기
const getGCD = (n, m) => {
    if (n % m === 0) {
        return m;
    } else {
        return getGCD(m, n % m);
    }
}

// 두 수의 곱을 최대 공약수로 나누어, 최소공배수 구하기
const getLCM = (n, m) => n * m / getGCD(n, m);

const solution = (denum1, num1, denum2, num2) => {
    const numLCM = getLCM(num1, num2);
    const numSum = (denum1 * (numLCM / num1)) + (denum2 * (numLCM / num2));
    const answerGCD = getGCD(numLCM, numSum);
    return [numSum / answerGCD, numLCM / answerGCD];
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

