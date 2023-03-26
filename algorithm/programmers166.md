

# [프로그래머스] 카드 뭉치 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (cards1, cards2, goal) => {
    // 순회할 각 cards의 index
    let cards1Index = 0;
    let cards2Index = 0;
    // goal을 만들 수 있는 지의 여부
    let flag = true;
    // goal 배열을 순회하며 카드를 만들 수 있는 지 확인
    for (let i = 0; i < goal.length; i++) {
        // 만들어야할 단어
        const word = goal[i];
        // cards1로 만들 수 있는 경우
        if (cards1[cards1Index] === word) {
            // 다음으로 넘어가기
            cards1Index += 1;
            continue;
        }
        // cards2로 만들 수 있는 경우
        if (cards2[cards2Index] === word) {
            // 다음으로 넘어가기
            cards2Index += 1;
            continue;
        }
        // 만들 수 없는 경우 중단
        flag = false;
        break;
    }
    return flag? 'Yes' : 'No';
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

