# [프로그래머스] 124 나라의 숫자 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(n) {
    let answer = '';
    // 124 나라의 숫자
    const numbers = [4, 1, 2];
    // n이 0이 되면 중단
    while (n !== 0) {
        // n을 3으로 나눈 몫
        let share = parseInt(n / 3);
        // n을 3으로 나눈 나머지
        const rest = n % 3;
        // 나머지가 0 인경우 몫에서 -1
        if (rest === 0) {
            share -= 1;
        }
        // 124 나라 숫자 입력
        answer = `${numbers[rest]}${answer}`
        // n을 몫으로 최신화
        n = share;
    }
    return answer;
}
```



## Comment

진법 변환 문제와 비슷한 느낌의 문제.
단, 진법의 경우 0이 존재하지만 이 문제에서는 0이 존재하지 않는다.
그래서 나머지가 0인 경우, 0을 표현해야 하지만 그럴 수 없으므로 몫에서 -1 처리를 한 뒤, 그 숫자로 숫자 변환을 이어서 진행한다.

## Reference

[프로그래머스](https://programmers.co.kr)

