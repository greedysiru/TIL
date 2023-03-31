

# [프로그래머스] 대충 만든 자판 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (keymap, targets) => {
    var answer = [];
    // keymap에서 각 알파벳을 얻기 위한 최소 키 입력수를 구하기
    const minKeyInputCount = keymap.reduce((obj, cur) => {
        // cur을 키 입력수로 변환
        for (const [index, alphabet] of Object.entries(cur)) {
            const inputCount = parseInt(index) + 1;
            // 최솟값인 경우에만 obj에 입력
            if (obj[alphabet] === undefined || obj[alphabet] > inputCount) {
                obj = {...obj,
                  [alphabet]: inputCount,
                }
            }
        }
        return obj;
    }, {});
    // targets을 위해 최소 몇 번씩 눌러야하는지 구하기
    const minCounts =  targets.map((str) => {
        return str.split('').reduce((acc, curStr) => {
            return acc + minKeyInputCount[curStr];
        }, 0);
    })
    return minCounts.map((cnt) => Number.isInteger(cnt)? cnt : -1);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

