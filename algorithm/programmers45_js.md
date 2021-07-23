# [프로그래머스] 숫자 문자열과 영단어 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 숫자 문자열과 영단어
function solution(s) {
  let answer = '';
  // 영단어에서 숫자를 표시한 객체
  const wordToNumber = {
    'zero': 0,
    'one': 1,
    'two': 2,
    'three': 3,
    'four': 4,
    'five': 5,
    'six': 6,
    'seven': 7,
    'eight': 8,
    'nine': 9,
  }
  // numbersToWrods의 키
  const wordToNumberKeys = Object.keys(wordToNumber);
  // 주어진 s를 순회
  // 넣을 단어
  let word = '';
  for (let chr of s) {
    // 숫자인 경우
    if (!isNaN(chr)) {
      // 단어 넣기
      answer += chr;
    } else {
      // 숫자가 아닌 경우
      word += chr;
      if (wordToNumberKeys.includes(word)) {
        answer += wordToNumber[word];
        word = '';
      }
    }
  }
  return parseInt(answer);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

