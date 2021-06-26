


# [프로그래머스] 다트 게임 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 다트 게임
function solution(dartResult) {
  let answer = 0;
  // 점수를 기록하는 배열
  const scoreArray = [];
  // 점수를 누적하는 변수
  let score = '';
  // dartResult의 길이
  dartResultLength = dartResult.length;
  for (let i = 0; i < dartResultLength; i++) {
    // 현재 접근한 결과
    const currentResult = dartResult[i]
    // S, D, T, *, # 중 하나인지 검사
    if (currentResult === 'S') {
      // socre를 scoreArray에 push
      scoreArray.push(parseInt(score));
      score = '';
    }
    else if (currentResult === 'D') {
      // score를 2제곱 후 scroeArray에 push하고 0으로 초기화
      scoreArray.push(parseInt(score) ** 2);
      score = '';
    }
    else if (currentResult === 'T') {
      // score를 3제곱 후 scoreArray에 push하고 0으로 초기화
      scoreArray.push(parseInt(score) ** 3);
      score = '';
    }
    // *인경우 기록된 점수를 2배처리
    else if (currentResult === '*') {
      // 현재 기록된 scoreArray의 길이
      scoreArrayLength = scoreArray.length;
      // 길이가 1이면 점수 하나만 2배 처리
      if (scoreArrayLength === 1) {
        scoreArray[0] *= 2;
      }
      // 1보다 큰 경우 이전 점수, 현재 점수 2배 처리
      else if (scoreArrayLength > 1) {
        scoreArray[scoreArrayLength - 1] *= 2;
        scoreArray[scoreArrayLength - 2] *= 2;
      }
    }
    // #인 경우 해당 점수 - 처리
    else if (currentResult === '#') {
      scoreArray[scoreArray.length - 1] *= -1;
    }
    // 위의 문자열이 아니면 숫자이므로 점수를 누적
    else {
      score += currentResult;
    }
  }
  answer = scoreArray.reduce((prev, curr) => prev + curr, 0)
  return answer;
}

```



## Comment

주어진 문자열을 크게 세가지로 분류하면 된다. S, D, T일 경우, *, #일 경우 그리고 숫자일 경우이다.

그리고 점수를 기록하기 위해서, 별도의 점수 배열을 만들고 숫자가 나올때는 누적을, 숫자가 아닐 때는 각각의 처리를 해주도록 한다.

점수는 누적해야하는데, 문자열 자료형을 가지는 변수를 선언하여 사용한다. 위부터 S, D, T, *, # 인 경우들을 필터링하고 처리하면 된다. 점수는 점수 배열에 기록하기 전에는 계속 문자열 처리하여 두자리인 경우도 잘 기록되도록 한다.

S, D, T의 경우에는 누적된 점수를 가져와 `parseInt`하여 각각 1, 2, 3제곱 후 점수 배열에 `append` 한다.

*의 경우에는 점수를 기록하는 배열의 길이에 따라서 처리한다. 배열의 길이가 1이면 0번 인덱스를 2배하면 되고 1을 초과하는 경우 배열의 길이 -1 번 인덱스, 배열의 길이 -2번 인덱스의 요소를 2배처리한다.

#의 경우는 가장 마지막에 위치한 점수 배열의 요소를 음수로 변환하도록 한다.

마지막에 배열의 합을 구하기 위해서는 `reduce`메소드를 사용하여 누적합을 return 하도록 한다.



## Reference

[프로그래머스](https://programmers.co.kr)

