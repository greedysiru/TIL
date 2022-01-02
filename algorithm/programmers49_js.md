# [프로그래머스] 나머지가 1이 되는 수 찾기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```javascript
// 나머지가 1이 되는 수 찾기
function solution(n) {
    let answer = 0;
    // 1 ~ n - 1까지 접근하여 n을 나누었을 때, 나머지가 1이 되도록 하는 가장 작은 자연수 구하기
    for (let i = 1; i < n; i++) {
        if (n % i === 1) {
            answer = i;
            break;
        }
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

