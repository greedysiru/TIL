# [프로그래머스] 두 정수 사이의 합 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(a, b) {
    const startNum = a < b ? a : b;
    const endNum = a < b? b: a;
    let answer = 0;
    for (let i = startNum; i <= endNum; i++) {
        answer += i;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

