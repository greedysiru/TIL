# [프로그래머스] 행렬의 덧셈 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 행렬의 덧셈
function solution(arr1, arr2) {
  let answer = [];
  // 배열의 각 요소 합치기
  for (let i = 0; i < arr1.length; i++) {
    // 각 배열의 row
    const arr1Row = arr1[i];
    const arr2Row = arr2[i];
    // answer에 빈 배열 넣기
    answer.push([]);
    // 각 배열의 요소에 접근하여 더하여 answer에 넣기
    for (let j = 0; j < arr1Row.length; j++) {
      answer[i].push(arr1Row[j] + arr2Row[j]);
    }
  }
  return answer;
}
```



## Comment

두 배열 `arr1`와 `arr2`는 2차원 배열이다. 그리고 서로 길이가 같으므로 `이중 for 문`으로 각 배열의 행에 먼저 접근하고 행의 각 요소에 접근하여 서로 더해준다. 그리고 구한 합을 `answer`에 `push`한다. 이때, `answer`도 이 두 배열과 똑같은 길이를 가지는 2차원 배열이므로 두 번째 `for`문 전에, 행이될 빈 배열을 넣어준다.



## 모범 답안

```JavaScript
function solution(arr1,arr2){
    return arr1.map((a,i) => a.map((b, j) => b + arr2[i][j]));
}
```



## Comment

`map`메소드를 사용하여 간결하게 풀 수 있다.

## Reference

[프로그래머스](https://programmers.co.kr)

