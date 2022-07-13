# [프로그래머스] 나누어 떨어지는 숫자 배열 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(arr, divisor) {
    const answer = arr
    .filter((number) => number % divisor === 0)
    .sort((a, b) => a - b);
    
    return answer.length > 0? answer : [-1];
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

