

# [프로그래머스] 겹치는 선분의 길이 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (lines) => {
  let answer = 0;

  // 1. 주어진 lines에서의 최댓값, 최솟값 구하기
  const max = Math.max(...lines.flat());
  const min = Math.min(...lines.flat());

  // 2. min <= i <= max 범위에 존재하는 수를 순회
  let prevI = null;
  for (let i = min; i <= max; i++) {
    // 3. lines를 순회하며 i가 각 line에 속하면 count
    let count = 0;
    let lastEnd = null;
    lines.forEach((line) => {
      const [start, end] = line;
      if (start <= i && i <= end) {
        // 3-1. 이전에 순회한 라인의 끝점과 겹치는 부분인 경우
        if (lastEnd !== null && lastEnd !== start) {
          count += 1;
        }
        // 3-2. 이전 라인과 겹치는 부분이 아닌 새로운 라인인 경우
        if (lastEnd === null) {
          count += 1;
        }
        lastEnd = end;
      }
    });

    // 4. count가 2 이상이면, 겹치는 선분
    if (count >= 2) {
      if (prevI === i - 1) {
        answer += 1;
      }
      prevI = i;
    }
  }

  return answer;
};

```



## Reference

[프로그래머스](https://programmers.co.kr)

