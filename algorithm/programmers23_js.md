# [프로그래머스] 오픈채팅방 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 오픈채팅방
function solution(record) {
  let answer = [];
  // 유저 아이디를 저장하는 해시
  const userId = {};
  // 유저 아이디가 최종으로 적용되기 전의 임시 메시지 배열
  const tempMessageArray = [];
  // 유저의 입장, 퇴장에 따른 문구
  const enterAndLeave = {
    Enter: '님이 들어왔습니다.',
    Leave: '님이 나갔습니다.'
  };
  // record를 하나씩 접근하여 최종 유저 닉네임 찾기
  for (let re of record) {
    const [state, uid, nickName] = re.split(' ');
    if (nickName !== undefined) {
      userId[uid] = nickName;
    }
    if (state === 'Enter' || state === 'Leave') {
      tempMessageArray.push([uid, state]);
    }
  }
  // 만들어진 tempMessageArray 접근하여 최종 메시지 만들기
  for (let tempMessage of tempMessageArray) {
    answer.push(`${userId[tempMessage[0]]}${enterAndLeave[tempMessage[1]]}`);
  }
  return answer;
}
```



## Comment

주어진 `Record`에서 사용자에게 보여줄 메시지를 만들기 위해 `for문`으로 접근하여 `split`을 사용하여 공백 기준으로 나누어준다. 이때 ,비구조화를 통해서 적절한 변수들에 할당한 후, 사용자의 닉네임을 가장 마지막에 설정된 닉네임으로 기록하도록 한다. 사용자 닉네임은 `사용자 아이디 : 닉네임`의 형식을 가지는 해시로 기록된다. 그리고 메시지를 출력해내기 위해서 `state`가 `Enter`, `Leave`인 경우 `tempMessageArray`에 `push` 한다.

`for문`이 끝나면, 유저 아이디별 닉네임은 적절한 것으로 최신화되어있으므로 최종 메시지를 출력하기 위해 `tempMessageArray`를 `for문`으로 하나씩 접근하여 리터럴 템플릿으로 문구를 `answer` 에 `push`한다.

## Reference

[프로그래머스](https://programmers.co.kr)

