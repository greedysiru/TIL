# [프로그래머스] 이상한 문자 만들기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 이상한 문자 만들기
function solution(s) {
  let answer = [];
  const sArray = s.split(' ');
  for (let i = 0; i < sArray.length; i++) {
    const character = sArray[i];
    let convertCharacter = '';
    for (let j = 0; j < character.length; j++) {
      if (j % 2 === 0) {
        convertCharacter += character[j].toUpperCase();
      } else {
        convertCharacter += character[j].toLowerCase();
      }
    }
    answer.push(convertCharacter);
  }
  return answer.join(' ');
}
```



## Comment

주어진 문자열을 `split`을 사용해 공백 기준으로 나누어준 뒤, 나누어진 각 문자열을 `for문`을 사용해 하나씩 접근한다. 그리고 다시 문자열의 한글자씩 `for문`으로 접근하고 `j`가 짝수일 때는 `toUpperCase`로 대문자 처리를, 홀수일 때는 `toLowerCase`로 소문자처리를 한다.

처리된 문자열은 `answer`에 `push`하고 모든 작업이 끝난 후에는 `join`으로 공백을 주어서 `return` 한다.

## Reference

[프로그래머스](https://programmers.co.kr)

