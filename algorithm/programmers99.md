# [프로그래머스] 튜플 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(s) {
    const answer = [];
    // 주어진 s를 배열로 변환
    const sArray = s
        // 필요없는 중괄호 제거
        .replace(/{{|}}/g, '')
        // 중괄호 묶음을 기준으로 배열로 변환
        .split('},{')
        // 각 요소들을 배열로 변환
        .map(elements => elements.split(','))
        // 배열 길이를 기준으로 오름차순 장렬
        .sort((a, b) => a.length - b.length < 0? -1 : 1)
        // 요소를 하나씩 순회하여 중복되지 않은 요소를 answer에 넣기
        .forEach(elements => elements.forEach(element => answer.indexOf(Number(element)) === -1 && answer.push(Number(element))));
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

