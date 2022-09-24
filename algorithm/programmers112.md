# [프로그래머스] 성격 유형 검사하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
// 성격 유형별 점수를 기록하는 객체
const scores = {
    'R': 0,
    'T': 0,
    'C': 0,
    'F': 0,
    'J': 0,
    'M': 0,
    'A': 0,
    'N': 0,
};

function solution(survey, choices) {
    var answer = '';
    // 주어진 survey, choices 순회
    survey.forEach((sur, idx) => {
        // 비동의 성격 유형
        const first = sur[0];
        // 동의 성격 유형
        const second = sur[1];
        // 선택한 점수
        const choice = choices[idx];
        if (choice < 4) {
            // 비동의 성격 유형 점수 더하기
            scores[first] += 4 - choice;
        } else if (choice > 4) {
            // 동의 성격 유형 점수 더하기
            scores[second] += choice - 4;
        }
    });

    if (scores['R'] >= scores ['T']) {
        answer += 'R';
    } 
    if (scores['R'] < scores ['T']) {
        answer += 'T';
    } 
    if (scores['C'] >= scores['F']) {
        answer += 'C';
    } 
    if (scores['C'] < scores['F']) {
        answer += 'F';
    } 
    if (scores['J'] >= scores['M']) {
        answer += 'J';
    } 
    if (scores['J'] < scores['M']) {
        answer += 'M';
    }
    if (scores['A'] >= scores['N']) {
        answer += 'A';
    } 
    if (scores['A'] < scores['N']) {
        answer += 'N';
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

