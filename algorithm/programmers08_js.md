


# [프로그래머스] 시저 암호 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 시저 암호
function solution(s, n) {
  let answer = '';
  // 입력받은 s를 하나씩 탐색
  for (let i = 0; i < s.length; i++) {
    // s의 각 문자를 아스키코드로 변환
    let sASCII = s.charCodeAt(i);
    // 대문자의 경우 65 ~ 90의 범위
    if (sASCII >= 65 && sASCII <= 90) {
      // n만큼 이동시키기
      sASCII += n;
      // 이동 후, 90을 초과하면 처음으로 돌아가서 미는 것이므로 -26
      if (sASCII > 90) {
        sASCII -= 26;
      }
    }
    // 소문자의 경우 97 ~ 122의 범위
    if (sASCII >= 97 && sASCII <= 122) {
      // n만큼 이동시키기
      sASCII += n;
      // 이동 후, 122을 초과하면 처음으로 돌아가서 미는 것이므로 -26
      if (sASCII > 122) {
        sASCII -= 26;
      }
    }
    // sASCII를 문자열로 변환 후 answer에 누적
    sString = String.fromCharCode(sASCII);
    answer += sString;
  }
  return answer;
}
```



## Comment

for문으로 주어진 문자열을 하나씩 접근하면서, `charCodeAt`메소드로 아스키코드로 변환한다. 이때 변환된 아스키코드의 범위가 65 ~ 90일 때는 대문자이고 97 ~ 122일 때는 소문자이다. 이 범위들에 들어올 때는 n만큼 더하고 각각 90, 122를 초과하면 문자가 처음부터 다시 돌아가는 것이므로 -26을 해준다.

처리한 아스키코드를 다시 문자열로 돌리는 `fromCharCode`메소드를 사용해서 변환 후, answer에 넣는다.



## Reference

[프로그래머스](https://programmers.co.kr)

