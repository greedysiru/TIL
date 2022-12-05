

# [프로그래머스] 가장 가까운 같은 글자 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (s) => s.split('').reduce((acc, cur, idx, origin) => {
    if (idx === 0) {
        return [-1];
    } else {
        const prevArray = origin.slice(0, idx);
        const lastIdx = prevArray.lastIndexOf(cur);
        const diffIdx = lastIdx !== -1? idx - lastIdx : lastIdx;
        return [...acc, diffIdx];
    }
}, []);
```



## Reference

[프로그래머스](https://programmers.co.kr)

