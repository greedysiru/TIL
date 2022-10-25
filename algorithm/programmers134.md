# [프로그래머스]  문자열 계산하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

##  문자열 계산하기

```JavaScript
const solution = (my_string) => my_string.split(' ').reduce((obj, cur, index, origin) => {
    let {acc, isPlus} = obj;
    if (cur === '+') {
        isPlus = true;
    } else if (cur === '-') {
        isPlus = false;
    } else if (isPlus === true) {
        acc += Number(cur);
    } else if (isPlus === false) {
        acc -= Number(cur);
    } else {
        acc += Number(cur);
    }
    return {acc, isPlus};
}, {acc: 0, isPlus: null}).acc;
```



## Reference

[프로그래머스](https://programmers.co.kr)

