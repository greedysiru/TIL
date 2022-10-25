# [프로그래머스]  문자열 계산하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

##  문자열 계산하기

```JavaScript
const solution = (numlist, n) => numlist.sort((a, b) => {
    const diff = Math.abs(n - a) - Math.abs(n - b);
    if (diff === 0) {
        return b - a;
    }
    return diff;
}); 
```



## Reference

[프로그래머스](https://programmers.co.kr)

