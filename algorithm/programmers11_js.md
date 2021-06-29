


# [프로그래머스] 완주하지 못한 선수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 완주하지 못한 선수
function solution(participant, completion) {
  let answer = '';
  // 입력받은 participant를 하나씩 접근하여 해시 만들기
  const playerHash = {}
  for (let player of participant) {
    if (!(player in playerHash)) {
      playerHash[player] = 1;
    } else {
      playerHash[player] += 1;
    }
  }
  // 완주한 선수 하나씩 접근
  for (let finishedPlayer of completion) {
    playerHash[finishedPlayer] -= 1;
  }
  // 완주하지 못한 선수 찾기
  for (let player of participant) {
    if (playerHash[player] > 0) {
      answer = player;
      break
    }
  }
  return answer;
}
```



## Comment

`participant` 를 하나씩 접근하여 참가자를 key로하고 같은 이름이 몇 명인지 기록된 해시를 만든다. 만들 때, 해시에 key가 없으면 value를 1로 초기화하고 있다면, value에 1을 더해준다. 

`completion`을 하나씩 접근하여 해시의 key에 넣어서 value를 -1한다. 그 이후, 다시 해시를 하나씩 접근하여 value가 0을 초과하는 경우 완주하지 못한 것이므로 해당 key를 answer에 담아 리턴한다.



## Reference

[프로그래머스](https://programmers.co.kr)

