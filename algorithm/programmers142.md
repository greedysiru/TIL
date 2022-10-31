# [프로그래머스] 팩토리얼 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const factorial = (n) => {
    if (n <= 1) {
        return 1;
    }
    
    return n * factorial(n - 1);
}

const solution = (n) => {
    let factorialResult = 0;
    let num = 1;
    while (true) {
        factorialResult = factorial(num);
        if (factorialResult > n) {
            num -= 1;
            break;
        }
        num += 1;
    }
    return num;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

