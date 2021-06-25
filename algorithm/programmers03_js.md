


# [프로그래머스] 연습문제: 소수 찾기- JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 소수 찾기
function solution(n) {
  let answer = 0;
  // n + 1 만큼의 길이를 가지는 배열 만들기
  nArray = new Array;
  // true는 소수라는 의미이며 기본 초기화 값
  for (let i = 0; i <= n; i++) {
    nArray[i] = true;
  }
  // 에라토스테네스의 체
  for (let j = 2; j <= Math.ceil(Math.sqrt(n)); j++) {
    // j번 인덱스가 소수이면 아래 명령을 실행
    if (nArray[j] === true) {
      k = 2;
      // j를 k를 곱해서 해당 요소 값을 false로 바꾸기(소수가 아니므로)
      while (j * k <= n) {
        nArray[j * k] = false;
        k += 1;
      }
    }
  }

  // 만들어진 소수 배열을 접근하여 개수 세기
  for (let l = 2; l <= n; l++) {
    if (nArray[l] === true) {
      answer += 1;
    }
  }
  return answer;
}
```



## Comment

주어진 숫자의 소수를 찾아 개수를 구하면 되는 문제. n+1만큼 길이를 가지는 배열을 각 요소가 true를 가지도록 초기화 한다. true는 소수일 때 표시하는 의미이다. 그 이후, 에라토스테네스로 2부터 n의 제곱근까지 만들어진 배열의 요소를 접근하여 요소의 값이 true일 때는 소수이므로 해당수를 2부터 곱해서 나오는 인덱스의 요소를 false로 바꾼다. 소수는 자기 자신과 1으로만 이루어져 있는데, 소수의 배수가 되면 소수가 아니기 때문이다.



# Reference

[프로그래머스](https://programmers.co.kr)

