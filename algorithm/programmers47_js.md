# [프로그래머스] 없는 숫자 더하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 없는 숫자 더하기
function solution(numbers) {
    let answer = 0;
    // 0 ~ 9까지 검사
    for (let i = 0; i <= 9; i++) {
        // numbers에 i가 없으면 answer에 더하기
        if (!numbers.includes(i)) {
            answer += i;
        }
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

