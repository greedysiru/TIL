# [프로그래머스] 예산 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(d, budget) {
    let answer = 0;
    // 1. d를 오름차순으로 정렬
    d.sort((a, b) => a - b);
    // 2. d를 하나씩 순회
    for (let m of d) {
        // 2-1. m이 예산보다 작으면 집행가능
        if (m <= budget) {
            budget -= m;
            answer += 1;
        } else if (m > budget) {
            // 2-2. 음수이면 예산을 초과했으므로 중단
            break;
        }
    }
    return answer;
}
```



## Comment

간단한 문제였으나, JavaScript 오름차순 정렬에서 헤메어 많은 시간이 소요되었다...

## Reference

[프로그래머스](https://programmers.co.kr)

