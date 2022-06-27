# [프로그래머스] 음양 더하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(absolutes, signs) {
    let answer = 0;
    absolutes.forEach((absolute, index) => answer += signs[index]? +absolute : -absolute);
    return answer;
}
```



## Comment

forEach문을 사용하여 명료하게 풀었다. forEach말고 reduce의 콜백 인수들을 사용하였으면 더 좋았을 것 같다.

## Reference

[프로그래머스](https://programmers.co.kr)

