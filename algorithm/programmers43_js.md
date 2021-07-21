# [프로그래머스] 방문 길이 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 방문 길이
function solution(dirs) {
  let answer = 0;
  // 캐릭터의 x, y 위치(처음)
  let positionX = 0;
  let positionY = 0;
  // 캐릭터가 움직인 경로 (정방향, 역방향)
  const route = [];
  // dirs 하나씩 접근
  for (let dir of dirs) {
    // U, 위로 이동
    if (dir === 'U') {
      // 전체 좌표를 넘는지 확인
      if ((positionY + 1) >= -5 && (positionY + 1) <= 5) {
        // 시작점
        const start = `${positionX}${positionY}`;
        positionY += 1;
        // 도착점
        const end = `${positionX}${positionY}`;
        // 이전의 이동 경로에 있는 지 확인
        if (!route.includes(start + end)) {
          // 이동한 경로가 아니므로 route에 push, answer +=1
          // 정방향, 역방향 둘 다 기록
          route.push((start + end), (end + start));
          answer += 1;
        }
      }
    }

    // D, 아래로 이동
    if (dir === 'D') {
      // 전체 좌표를 넘는지 확인
      if ((positionY - 1) >= -5 && (positionY - 1) <= 5) {
        // 시작점
        const start = `${positionX}${positionY}`;
        positionY -= 1;
        // 도착점
        const end = `${positionX}${positionY}`;
        // 이전의 이동 경로에 있는 지 확인
        if (!route.includes(start + end)) {
          // 이동한 경로가 아니므로 route에 push, answer +=1
          // 정방향, 역방향 둘 다 기록
          route.push((start + end), (end + start));
          answer += 1;
        }
      }

    }
    // R, 오른쪽으로 이동
    if (dir === 'R') {
      // 전체 좌표를 넘는지 확인
      if ((positionX + 1) >= -5 && (positionX + 1) <= 5) {
        // 시작점
        const start = `${positionX}${positionY}`;
        positionX += 1;
        // 도착점
        const end = `${positionX}${positionY}`;
        // 이전의 이동 경로에 있는 지 확인
        if (!route.includes(start + end)) {
          // 이동한 경로가 아니므로 route에 push, answer +=1
          // 정방향, 역방향 둘 다 기록
          route.push((start + end), (end + start));
          answer += 1;
        }
      }
    }

    // L, 왼쪽으로 이동
    if (dir === 'L') {
      // 전체 좌표를 넘는지 확인
      if ((positionX - 1) >= -5 && (positionX - 1) <= 5) {
        // 시작점
        const start = `${positionX}${positionY}`;
        positionX -= 1;
        // 도착점
        const end = `${positionX}${positionY}`;
        // 이전의 이동 경로에 있는 지 확인
        if (!route.includes(start + end)) {
          // 이동한 경로가 아니므로 route에 push, answer +=1
          // 정방향, 역방향 둘 다 기록
          route.push((start + end), (end + start));
          answer += 1;
        }
      }
    }
  }
  return answer;
}
```



## Comment

`dirs`를 하나씩 접근하며 캐릭터의 좌표가 범위를 벗어나지 않는지 확인하고 이동처리한다. 그리고 이동 경로를 기록할 때, 정방향과 역방향을 같이 기록해야 추후, 경로 카운트가 겹치지 않는다.



## Reference

[프로그래머스](https://programmers.co.kr)

