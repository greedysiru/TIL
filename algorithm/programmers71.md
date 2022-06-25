# [프로그래머스] 짝지어 제거하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(string) {
    // 짝을 집어 넣을 배열
    const pairArray = [];
    // 주어진 문자열 순회
    for (let s of string) {
        // pairArray가 비어있으면 현재 접근한 넣기
        if (!pairArray.length) {
            pairArray.push(s);
          // pairArray에 마지막에 넣은 문자가 현재 접근한 문자와 같을 때 
        } else if (pairArray[pairArray.length - 1] === s) {
            // 짝이 맞으므로 pairArray에서 삭제
            pairArray.pop();
          // pairArray에 마지막에 넣은 문자가 현재 접근한 문자와 다를 때
        } else {
            // 문자 넣기
            pairArray.push(s);
        }
    }
    // 순회 완료 후, pairArray의 길이가 0이면 짝지어 제거하기가 가능한 문자열
    if (!pairArray.length) {
        return 1;
    } else {
        return 0;
    }
}
```



## Comment

문자열을 하나씩 접근하면서 이전의 문자열과 짝이 맞는지 검사하는 로직을 수행한다. 이를 위해서, 문자열을 담아 짝을 체크할 별도 배열을 정의하고 반복문으로 주어진 문자열을 순회한다.

## Reference

[프로그래머스](https://programmers.co.kr)

