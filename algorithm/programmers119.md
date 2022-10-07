# [프로그래머스] 가장 먼 노드 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```javascript
const solution = (common) => {
    // 등차수열인지 등비수열인지 판별
    const first = common[0];
    const second = common[1];
    const third = common[2];
    const difference1 = second - first;
    const difference2 = third - second;
    // 다음에 올 수
    let nextNumber = common[common.length - 1];
    // 두 차이가 같으면 등차수열
    if (difference1 === difference2) {
        const difference = difference1;
        nextNumber += difference;
    } else {
        // 두 차이가 같지 않으면 등비수열
        const equalRatio = third / second;
        nextNumber *= equalRatio;
    }
    return nextNumber;
} 
```



## Reference

[프로그래머스](https://programmers.co.kr)

