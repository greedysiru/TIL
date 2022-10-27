# [프로그래머스]  합성수 찾기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (n) => {
    let synCnt = 0;
    for (let i = 1; i <= n; i++) {
        let cnt = 0;
        for (let j = 1; j <= i; j++) {
            if (i % j === 0) {
                cnt += 1;
            }
            if (cnt >= 3) {
                synCnt += 1;
                break;
            }
        }
    }
    return synCnt;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

