# [프로그래머스]  자동완성 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
class Node {
    constructor(value = [0, '']) {
        this.value = value;
        this.children = new Map();
    }
}

class Trie {
    constructor() {
        this.root = new Node();
    }
    
    insert(string) {
        let currentNode = this.root;
        
        for (const char of string) {
            if (!currentNode.children.has(char)) {
                currentNode.children.set(
                    char,
                    new Node([1 , currentNode.value[1] + char])
                );
            } else {
                const childrenNode = currentNode.children.get(char);
                childrenNode.value[0] += 1;
            }
            currentNode = currentNode.children.get(char);
        }
    }
    
    isSearchable(string) {
        let currentNode = this.root;
        for (const char of string) {
            if (!currentNode.children.has(char)) {
                return false;
            }
            currentNode = currentNode.children.get(char);
            if (currentNode.value[0] === 1) {
                return true;
            }
        }
        return false;
    }
}

function solution(words) {
    var answer = 0;
    const trie = new Trie();
    // 학습 시키기
    words.forEach(word => trie.insert(word));
    // 단어를 찾을 때 입력해야할 총 문자수 구하기
    // words.forEach(word => trie.has(word));
    for (const word of words) {
        let accW = '';
        let isSearchable = false;
        for (const currW of word) {
            accW += currW;
            isSearchable = trie.isSearchable(accW);
            if (trie.isSearchable(accW)) {
                answer += accW.length;
                break;
            }
        }
        if (!isSearchable) {
            answer += word.length;
        }
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

