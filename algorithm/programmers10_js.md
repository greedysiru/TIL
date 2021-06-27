


# [프로그래머스] 비밀지도 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 비밀 지도
function solution(n, arr1, arr2) {
  let answer = [];
  for (let i = 0; i < n; i++) {
    // 입력받은 두 array의 수를 하나씩 가져와서 이진법 변환
    // 0을 채워서 자릿수 맞추기
    const arr1Bin = arr1[i].toString(2).padStart(n, 0);
    const arr2Bin = arr2[i].toString(2).padStart(n, 0);
    // 만들어진 두 이진수(문자열)을 한글자씩 접근하여 비교하기
    // 둘 중 하나라도 1이면 #(벽), 둘다 0인경우 공백
    // 지도의 한 줄
    let map_row = '';
    for (let j = 0; j < n; j++) {
      if (arr1Bin[j] === '1' || arr2Bin[j] === '1') {
        map_row += '#';
      }
      else {
        map_row += ' ';
      }
    }
    answer.push(map_row);
  }
  return answer;
}
```



## Comment

주어진 두 배열의 요소를 `for문`으로 각각 접근하여 `toString` 메소드를 사용하여 문자열 형태인 이진수로 변환한다. 그리고 만들어진 이진수의 자릿수를 n만큼 채워야 하므로 `padStart` 메소드를 사용하여 ,비어있는 곳을 0으로 채운다.

만들어진 이진수를 for문으로 한글자씩 접근하여 둘 중 하나라도 1이면, 벽이 있는 것이므로 문자열 #을 만들어주고 아닌 경우, 공백을 넣어준다. 이렇게 가장 상위의 `for문`의 한 루프가 끝나면 만들어진 행정보를 `answer`에 `push`한다.



## Reference

[프로그래머스](https://programmers.co.kr)

