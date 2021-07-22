# [프로그래머스] 이진 변환 반복하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 이진 변환 반복하기
function solution(s) {
  let answer = [];
  // 0을 세는 카운터
  let countZero = 0;
  // 변환 횟수
  let countConvert = 0;
  // s를 담을 변수(배열로 변환 예정)
  let sArr = s
  // 1이 될때까지 실행
  while (sArr !== '1') {
    // 0을 제거
    sArr = sArr.split('').filter((val) => {
      // 0인 요소 세기
      if (val === '0') {
        countZero += 1;
      }
      // 0이 아닌 것만 return
      return val !== '0';
    }).length.toString(2)
    // 변환 횟수 카운트
    countConvert += 1;
  }
  return [countConvert, countZero];
}
```



## Comment

`dirs`를 하나씩 접근하며 캐릭터의 좌표가 범위를 벗어나지 않는지 확인하고 이동처리한다. 그리고 이동 경로를 기록할 때, 정방향과 역방향을 같이 기록해야 추후, 경로 카운트가 겹치지 않는다.



## Reference

[프로그래머스](https://programmers.co.kr)

