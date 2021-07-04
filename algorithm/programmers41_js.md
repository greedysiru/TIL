# [프로그래머스] 올바른 괄호 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 올바른 괄호
function solution(s) {
  let answer = true;
  // s를 배열에 넣기
  const sArray = s.split('');
  // 올바른 괄호인지 검사
  // 빼낸 괄호를 임시로 넣는 배열
  const sTemp = [];
  for (let i = 0; i < sArray.length; i++) {
    if (sArray[i] === '(') {
      sTemp.push(sArray[i]);
    } else {
      if (sTemp[sTemp.length - 1] === '(') {
        sTemp.pop();
      } else {
        sTemp.push(sArray[i]);
      }
    }
  }
  return sTemp.length === 0 ? true : false;
}
```



## Comment

주어진 `s`를 배열로 변환하고 `for문`으로 하나씩 접근한다. 여는 괄호가 오면 `sTemp`에 `push`하고, 닫는 괄호가 오는 경우 `sTemp`가 오면 `pop`을 한다. 그렇지 않다면, 해당 요소를  `sTemp`에 `push` 한다. 괄호가 짝이 맞다면, 반복문이 끝났을 때 `sTemp`의 `length`가 0일 것이고 아니라면 0을 초과할 것이다. 그것에 맞춰 `true, false`를 `return`한다.



## Reference

[프로그래머스](https://programmers.co.kr)

