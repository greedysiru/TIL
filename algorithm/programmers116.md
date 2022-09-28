# [프로그래머스]  입국심사 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
function solution(n, times) {
    // 모든 사람이 심사를 받는데 걸리는 시간의 최솟값은 1분 ~ (times에서 가장 큰 수 *  n)분의 범위에 속함
    // 가능한 최솟값 범위의 초기화
    let min = 1;
    let max = Math.max(...times) * n;
    
    // 이진탐색
    while (min <= max) {
        const mid = Math.floor((min + max) / 2);
        // 시간 / 각 심사관이 걸리는 시간 : 심사관당 처리 가능한 입국자 수
        // 현재 mid 시간을 기준으로 처리 가능한 입국자 수
        const sum = times.reduce((acc, cur) => acc + Math.floor(mid / cur), 0);
        
        if (sum < n) {
            // n보다 적으므로 min을 mid + 1로
            min = mid + 1;
        } else {
            // n보다 더 많으므로 max를 mid - 1로
            max = mid - 1;
        } 
    }
    return min;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

