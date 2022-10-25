# [프로그래머스]  컨트롤 제트 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (s) => s.split(' ').reduce((obj, cur) => {
    let {acc, arr} = obj;
    if (cur === 'Z') {
        acc -= arr.pop();
    } else {
        const curNumber = Number(cur);
        acc += curNumber;
        arr.push(curNumber);
    }
    return {acc, arr}
}, {acc: 0, arr: []}).acc;
```



## Reference

[프로그래머스](https://programmers.co.kr)

