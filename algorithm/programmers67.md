# [프로그래머스] 하노이의 탑 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 하노이의 탑
function solution(n) {
    const answer = [];
    // from: 원반의 출발 기둥, to: 목표 기둥 other: 목표 기둥, disc: 원반 갯수
    function hanoi(from, to, other, disc) {
        // 재귀 함수 호출 종료
        if (disc === 0) {
            return;
        } else {
            // 원반 하나를 제외하고 목적지가 아닌 곳으로 이동시킴
            hanoi(from, other, to, disc - 1);
            // 맨 아래 원반을 목적지로 이동시킴
            answer.push([from, to]);
            // 다른 곳으로 옮겼던 원반을 목적지로 이동시킴
            hanoi(other, to, from, disc - 1);
        }
    }
    // 재귀 함수 호출
    hanoi(1, 3, 2, n);
    return answer;
}
```



## Comment

오랜만에 재귀함수 문제를 풀려니 쉽지 않았다.

예전에 보았던 좋은 강의를 한 번 더...
[얄팍한 코딩 - 재귀함수](https://www.youtube.com/watch?v=aPYE0anPZqI)

## Reference

[프로그래머스](https://programmers.co.kr)

