# [프로그래머스] 문자열 내 마음대로 정렬하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(strings, n) {
    return strings.sort((a, b) => {
        const comparedNumber = a.charCodeAt(n) - b.charCodeAt(n);
        if (comparedNumber === 0) {
            if (a > b) return 1;
            if (b > a) return -1;
        }  else {
            return comparedNumber;
        }
    });
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

