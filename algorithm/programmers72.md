# [프로그래머스] 영어 끝말잇기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(n, words) {
    const answer = [];

    // 1. 참여자들이 말했던 단어를 기록할 배열
    const saidWords = new Array();
    
    // 2. words 하나씩 접근
    for (let i = 0; i < words.length; i++) {
        // saidWord 초기화
        if (!saidWords.length) {
            saidWords.push(words[i]);
            continue;
        };
        
        // 2-1. 끝말잇기가 유효한지 검삭
        // 마지막에 말한 단어
        const lastSaidWord = saidWords[saidWords.length - 1];
        // 마지막에 말한 단어의 끝과 현재 말한 단어의 처음 비교하여, 다른 경우
        if (lastSaidWord[lastSaidWord.length - 1] !== words[i][0]) {
            answer.push((i + 1) % n || n);
            answer.push(parseInt(i / n + 1));
            break;
        }
        // 2-2. 중복여부
        if (saidWords.indexOf(words[i]) !== -1) {
            answer.push((i + 1) % n || n);
            answer.push(parseInt(i / n + 1));
            break;
        }
        
        // 탈락자가 발생하지 않은 경우 saidWords에 push
        saidWords.push(words[i]);
    }
    // saidWords의 길이와 words의 길이가 같으면 탈락자가 없음
    if (saidWords.length === words.length) {
        answer.push(0, 0);
    }
    return answer;
}
```



## Comment

주어진 단어들을 순회하며 1. 끝말잇기 조건에 맞는지 2. 중복된 단어를 안 말했는지 두 가지 조건을 확인하면 된다.

## Reference

[프로그래머스](https://programmers.co.kr)

