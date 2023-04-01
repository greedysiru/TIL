

# [프로그래머스] 기사단원의 무기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (number, limit, power) => {
  let ironWeight = 0;
  const divisorCounts = getDivisorCounts(number);

   // 필요한 철 구하기
  for (let i = 1; i <= number; i++) {
    // 현재 기사의 공격력
    const divisorCount = divisorCounts[i];
    // limit를 초과하는 경우 power를 넣기 
    const attackPower = divisorCount > limit ? power : divisorCount;
    ironWeight += attackPower;
  }

  return ironWeight;
}

// number까지의 모든 수에 대해 약수의 계수를 미리 계산
const getDivisorCounts = (number) => {
  const divisorCounts = new Array(number + 1).fill(0);

  for (let i = 1; i <= number; i++) {
    for (let j = i; j <= number; j += i) {
      divisorCounts[j]++;
    }
  }

  return divisorCounts;
}

```



## Reference

[프로그래머스](https://programmers.co.kr)

