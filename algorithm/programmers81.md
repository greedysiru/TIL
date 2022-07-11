# [프로그래머스] 가운데 글자 가져오기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(s) {
    let answer;
    const lengthForS = s.length;
    const isEven = lengthForS % 2 === 0;
    if (isEven) {
        answer = s.slice((lengthForS / 2 - 1), (lengthForS / 2 + 1))
    } else {
        answer = s[(lengthForS - 1) / 2];
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

