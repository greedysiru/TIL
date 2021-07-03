# [프로그래머스] 핸드폰 번호 가리기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 핸드폰 번호 가리기
function solution(phone_number) {
  let answer = '';
  // 전화번호의 길이
  const phoneNumberLength = phone_number.length;
  // 번호 가리기
  for (let i = 0; i < phoneNumberLength; i++) {
    if (i < phoneNumberLength - 4) {
      answer += '*';
    } else {
      answer += phone_number[i];
    }
  }
  return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

