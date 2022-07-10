# [프로그래머스] 문자열 내 p와 y의 개수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(s){
    // p의 갯수
    let pEA = 0;
    // y의 갯수
    let yEA = 0;
    // 문자열 -> 배열 -> forEach로 순회
    s.split('').forEach((string) => {
        const convertedString = string.toLowerCase();
        if (convertedString === 'p') pEA += 1;
        if (convertedString === 'y') yEA += 1;
    })
    return pEA === yEA;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

