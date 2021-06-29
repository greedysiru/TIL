


# [프로그래머스] k번째수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// k번째수
function solution(array, commands) {
  let answer = [];
  // 2차원 배열 commands를 하나씩 접근
  for (let command of commands) {
    // 시작 인덱스
    const start = command[0] - 1;
    // 끝 인덱스
    const end = command[1];
    // 뽑을 인덱스
    const pick = command[2] - 1;
    // 배열 슬라이싱
    const arraySlice = array.slice(start, end);
    // 정렬
    arraySlice.sort((a, b) => a - b);
    // 뽑아낸 원소 넣기
    answer.push(arraySlice[pick]);
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

