# [프로그래머스] 두 개 뽑아서 더하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(numbers) {
    const answer = [];
    // numbers의 길이
    const numbersLength = numbers.length;
    // 1. numbers 순회
    for (let i = 0; i < numbersLength; i++) {
        // 1-1. 첫번째로 선택한 수
        const firstNum = numbers[i];
        // 2. 첫번째로 선택한 수 이후의 numbers 배열을 순회
        for (let j = i + 1; j < numbersLength; j++) {
            // 2-1. 두번째로 선택한 수
            const secondNum = numbers[j];
            // 2-2. 두 수의 합
            const sumNum = firstNum + secondNum;
            // 3. 두 수의 합이 answer 배열에 없는 경우에만 answer배열에 push
            if (!answer.includes(sumNum)) {
                answer.push(sumNum);
            }
        }
    }
    // 오름 차순 정렬
    answer.sort((a, b) => a - b);
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

