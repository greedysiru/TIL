# [프로그래머스] 문자열 다루기 기본 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(s) {
    let answer = true;
    const sLength = s.length;
    if (sLength === 4 || sLength === 6) {
        for (let i = 0; i < sLength; i++) {
            if (isNaN(s[i])) {
                answer = false;
                break;
            }
        }
    } else {
        answer = false;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

