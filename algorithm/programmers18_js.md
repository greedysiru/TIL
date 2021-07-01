
# [프로그래머스] 가장 큰 수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 가장 큰 수
function solution(numbers) {
  // number의 요소를 string화
  const numbersString = numbers.map((num) => String(num));
  // 정렬하기
  numbersString.sort((a, b) => {
    // b + a숫자와 a + b 숫자를 비교해서 내림차순으로 정렬
    return parseInt(b + a) - parseInt(a + b);
  })
  // 만들어진 배열 문자열화
  const answer = numbersString.join('');
  return answer[0] === '0' ? '0' : answer;
}
```



## Comment

주어진 `numbers`  배열의 요소를 문자열로 바꾸어준다.

문자열로 이루어진 `numberString`배열을 정렬하는데, 각 요소는 문자열이므로 `+` 연산으로 붙여줄 수 있다. `sort`메소드의 a, b 파라미터를 가져와서 b + a 숫자와 a + b 숫자를 `partInt`하여 내림차순으로 정렬될 수 있도록 `return` 한다.

## Reference

[프로그래머스](https://programmers.co.kr)

