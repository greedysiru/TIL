


# [프로그래머스] 위장 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 위장
function solution(clothes) {
  let answer = 1;
  // clothes 해시 만들기
  // key: 의상의 종류, value: 의상 배열
  const clothesHash = {};
  for (let cloth of clothes) {
    if (!(cloth[1] in clothesHash)) {
      clothesHash[cloth[1]] = [cloth[0]];
    }
    else {
      clothesHash[cloth[1]].push(cloth[0]);
    }
  }
  // 조합 세기
  for (let cloth in clothesHash) {
    const clothEA = clothesHash[cloth].length;
    answer *= clothEA + 1
  }
  return answer - 1;
}
```



## Comment

key를 의상의 종류로 하고 value를 의상 배열로 하는 해시를 만든다. 만들어진 해시를 토대로 조합의 수를 구한다. 조합의 수는 각 옷의 수 + 1한 수를 누적해서 곱하고 최종적으로 -1을 한다.

> **옷 조합의 수 = (각 종류별 옷의 수 + 1) * (각 종류별 옷의 수 + 1) ... - 1**
>
> **+1은 해당 옷을 안 입었을 때의 경우의 수**
>
> **-1은 전부 한 입었을 때의 경우의 수**



## Reference

[프로그래머스](https://programmers.co.kr)

