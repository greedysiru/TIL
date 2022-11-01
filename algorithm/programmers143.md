# [프로그래머스] 저주의 숫자 3 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (n) => {
    let number3x = 0;
    for (let i = 1; i <= n; i++) {
        number3x += 1;
        while (number3x % 3 === 0 || number3x.toString().includes('3')) {
            number3x += 1;
        }
    }
    return number3x;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

