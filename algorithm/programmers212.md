

# [프로그래머스] 수 조작하기 1

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (n, control) => {
    // control에 따른 연산
    const controlLookupTable = {
        'w': 1,
        's': -1,
        'd': 10,
        'a': -10,
    }
    return control.split('').reduce((acc, cur) => acc + controlLookupTable[cur], n);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

