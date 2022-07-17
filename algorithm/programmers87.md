# [프로그래머스] 콜라츠 추측 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(num) {
    let count = 0;
    function collatz(num){
    // num이 1이면 중단
    if (num === 1) {
        return;
    }
    // count가 500이면 중단
    if (count === 500) {
        count = -1;
        return;
    }
    count += 1;
    const isEven = num % 2 === 0;
    if (isEven) {
        const dividedNum = num / 2;
        collatz(dividedNum);
    } else {
        const multipliedNum = num * 3 + 1;
        collatz(multipliedNum);
    }
}
    collatz(num);
    return count;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

