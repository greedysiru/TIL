

# [프로그래머스] 문자열 나누기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
function solution(s) {
    let answer = 0;
    // 글자 x
    let x = s[0];
    // 글자 x count
    let xCount = 0;
    // 다른 글자 count
    let diff = 0;
    // s를 순회
    for (let i = 0; i < s.length; i++) {
        // 현재 접근한 문자
        const curString = s[i];
        // x와 같으면 xCount + 1
        if (x === curString) {
            xCount += 1;
        } else {
            diff += 1;
        }
        // xCount, diff가 같으면 분리
        if (xCount === diff) {
            answer += 1;
            // 모두 초기화
            xCount = 0;
            diff = 0;
            console.log(x)
            x = s[i + 1];
        }
        // 순회가 끝났을 때, 나머지도 분해되므로 count
        if (i === s.length - 1 && (xCount !== diff)) answer += 1; 
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

