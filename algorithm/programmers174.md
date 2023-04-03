

# [프로그래머스] 귤 고르기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (k, tangerine) => {
    // 과일 종류별로 개수를 세어 fruitCount 객체에 저장
    const fruitCount = {};
    for (const fruit of tangerine) {
        if (fruitCount[fruit]) {
            fruitCount[fruit]++;
        } else {
            fruitCount[fruit] = 1;
        }
    }
    
    // 과일 개수가 많은 순서대로 정렬
    const sortedFruit = Object.entries(fruitCount).sort((a, b) => b[1] - a[1]);
    let selectedCount = 0;
    let selectedFruit = [];
    // 선택된 과일 종류와 개수를 저장
    for (const [fruit, count] of sortedFruit) {
        // 선택할 과일 개수가 남아있으면, 현재 과일 개수와 선택할 과일 개수 중 작은 값만큼 선택
        const remainingCount = Math.min(count, k - selectedCount);
        selectedCount += remainingCount;
        selectedFruit.push(fruit);
        // 모든 과일을 선택했으면 종료
        if (selectedCount === k) {
            break;
        }
    }
    
    // 선택한 과일 종류의 개수를 반환
    return selectedFruit.length;
}

```



## Reference

[프로그래머스](https://programmers.co.kr)

