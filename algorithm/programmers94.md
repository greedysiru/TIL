# [프로그래머스] 키패드 누르기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
// 스마트폰 키패드
// key: 키패드 번호
// value: 키패드의 2차원 좌표
const keyPad = {
        1: [0, 0],
        2: [0, 1],
        3: [0, 2],
        4: [1, 0],
        5: [1, 1],
        6: [1, 2],
        7: [2, 0],
        8: [2, 1],
        9: [2, 2],
        '*': [3, 0],
        0: [3, 1],
        '#': [3, 2]
    }

function solution(numbers, hand) {
    let answer = '';
    // 각 손가락의 위치
    let leftHandPosition = [3, 0];
    let rightHandPosition = [3, 2];
    // 누를 keyPad의 위치
    let keyPadPosition;
    // 주어진 numbers를 순회
    numbers.forEach((num) => {
        keyPadPosition = keyPad[num];
        // keyPad의 위치의 1번 index가 0이면 L(왼쪽)
            if (keyPadPosition[1] === 0) {
                answer += 'L';
                leftHandPosition = keyPadPosition;
                // 1번 index가 2이면 R(오른쪽)
            } else if (keyPadPosition[1] === 2) {
                answer += 'R';
                rightHandPosition = keyPadPosition;
            } else {
                // 2, 5, 8, 0의 경우 keyPadPosition기준으로 거리를 계산하기
                const leftDistance = Math.abs(keyPadPosition[0] - leftHandPosition[0]) + Math.abs(keyPadPosition[1] - leftHandPosition[1]);
                const rightDistance = Math.abs(keyPadPosition[0] - rightHandPosition[0]) + Math.abs(keyPadPosition[1] - rightHandPosition[1]);
                // 거리가 짧은 손가락이 이동
                if (leftDistance < rightDistance) {
                    answer += 'L';
                    leftHandPosition = keyPadPosition;
                } else if (leftDistance > rightDistance) {
                    answer += 'R';
                    rightHandPosition = keyPadPosition;
                    // 서로 거리가 같은 경우 어느 손잡이인지를 기준으로 이동
                } else if (leftDistance === rightDistance) {
                    if (hand === 'left') {
                        answer += 'L';
                        leftHandPosition = keyPadPosition;
                    } else {
                        answer += 'R';
                        rightHandPosition = keyPadPosition;
                    }
                }
            }
    });
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

