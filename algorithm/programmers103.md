# [프로그래머스]  모음 사전 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(word) {
    // 알파벳 모음
    const alphabet = ['A', 'E', 'I', 'O', 'U'];
    let count = 0;
    let endFlag = false;
    // 단어를 만드는 DFS
    function DFS(makedWord) {
        if (makedWord === word || endFlag) {
            endFlag = true;
            return;
        }
        if (makedWord.length > 5){
            return;
        }
        count += 1;
        for (let i = 0; i < alphabet.length; i++) {
            DFS(`${makedWord}${alphabet[i]}`);
        }
    }
    DFS('');
    return count;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

