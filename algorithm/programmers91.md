# [프로그래머스] 폰켓몬 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(nums) {
    const pickableNumber = nums.length / 2;
    const ponketMonSet = new Set(nums);
    return Math.min(pickableNumber, ponketMonSet.size);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

