# [프로그래머스] 타겟 넘버 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
function solution(numbers, target) {
    let answer = 0;
    // 주어진 숫자의 개수
    const numbersCount = numbers.length;
    // index: 접근할 배열의 인덱스, numbers: 주어진 숫자 배열, sum: 누적된 합, target: 목표합
    function DFS(index, sum) {
        // 주어진 숫자 배열을 탐색 완료하면
        if (index === numbersCount) {
            // target과 같으면 답으로 기록
            if (sum === target) {
                answer += 1;
            }
            // 재귀 호출 종료
            return;
        } else {
            // 숫자 배열의 다음 인덱스에 접근하고 누적합에 더하기
            DFS(index + 1, sum + numbers[index]);
            // 숫자 배열의 다음 인덱스에 접근하고 누적합에 빼기
            DFS(index + 1, sum - numbers[index]);
        }
    }
    DFS(0, 0);
    return answer;
}
```



## Comment

DFS를 활용해서 주어진 수들로 구할 수 있는 모든 합의 케이스를 구하고, target에 맞는 경우 카운트하도록 처리하였다.

재귀적으로 케이스를 분할해서 접근한다는 개념으로 풀었다.

## Reference

[프로그래머스](https://programmers.co.kr)

