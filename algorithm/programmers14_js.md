


# [프로그래머스] 기능개발 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 기능개발
function solution(progresses, speeds) {
  let answer = [];
  // progresses가 존재하면 실행
  while (progresses.length > 0) {
    // 가장 맨 앞의 요소가 100보다 아래일 떄
    while (progresses[0] < 100) {
      // 각 요소에 해당하는 speeds 요소 더하기
      for (let i = 0; i < progresses.length; i++) {
        progresses[i] += speeds[i];
      }
    }
    // 완료된 작업 수
    let complitedProgress = 0;
    // 가장 맨 앞의 요소가 100이상이면 실행
    while (progresses[0] >= 100) {
      // 가장 앞 요소 빼기
      progresses.shift();
      speeds.shift();
      // 뺀 만큼 완료된 작업 수 기록
      complitedProgress += 1;
    }
    answer.push(complitedProgress);
  }
  return answer;
}
```



## Comment

작업은 완료되어도 가장 맨 왼쪽에 있는 것부터 배포될 수 있으므로 큐 자료구조형 아이디어를 사용한다.

모든 작업을 다 처리할때까지 처리하는 것이므로 progresses의 length 프로퍼티가 0보다 클때 전체 루프를 반복하도록 한다. `for 문`을 사용해서 각 작업에 해당하는 speeds의 요소를 매번 더해준다. 만약, 가장 맨앞의 요소가 100이 이상이면 `while문`의 조건을 설정하여 가장 앞 요소를 계속 빼서 그 시점의 배포 가능한 작업의 수를 answer에 기록한다.



## Reference

[프로그래머스](https://programmers.co.kr)

