# [프로그래머스] 3진법 뒤집기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(n) {
    var answer = 0;
    // 1. n을 3진법으로 변환한 수
    const ternary = n.toString(3);
    // 2. ternary를 반대로 뒤집기
    const reverseTernary = ternary.split('').reverse().join('');
    // 3. reverseTernary를 10진법으로 변환
    const decimal = parseInt(reverseTernary, 3);
    return decimal;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

