

# [프로그래머스] 마지막 두 원소

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (숫자들) => {
    const 마지막원소 = 숫자들[숫자들.length - 1];
    const 마지막전원소 = 숫자들[숫자들.length - 2];
    마지막원소 > 마지막전원소? 숫자들.push(마지막원소 - 마지막전원소) : 숫자들.push(마지막원소 * 2);
    return 숫자들;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

