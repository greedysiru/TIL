# [프로그래머스]  숫자의 표현 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(n) {
    var answer = 0;
    // n까지의 연속한 숫자를 가지는 배열
    const numberArray = new Array(n).fill(0).map((_, index) => index + 1);
    // 연속한 자연수로 n을 표현할 방법 찾기
    let startIndex = n - 1;
    while (startIndex >= 0) {
        let sum = 0;
        for (let i = startIndex; i >= 0; i--) {
            sum += numberArray[i];
            if (sum === n) {
                answer += 1;
            }
            if (sum > n) {
                break;
            }
        }
        startIndex -= 1;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

