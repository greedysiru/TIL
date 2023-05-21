

# [프로그래머스] 주사위 게임 1

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (숫자1, 숫자2) => {
    const 숫자1홀수인지 = 숫자1 % 2 === 1;
    const 숫자2홀수인지 = 숫자2 % 2 === 1;
    
    if (숫자1홀수인지 && 숫자2홀수인지) return 숫자1**2 + 숫자2**2;
    else if (숫자1홀수인지 || 숫자2홀수인지) return 2 * (숫자1 + 숫자2);
    else return Math.abs(숫자1 - 숫자2);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

