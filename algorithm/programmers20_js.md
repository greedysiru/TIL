# [프로그래머스] 모의고사 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 모의고사
function solution(answers) {
  let answer = [];
  // 1번 수포자 ~ 3번 수포자
  const oneSupo = [1, 2, 3, 4, 5];
  const twoSupo = [2, 1, 2, 3, 2, 4, 2, 5];
  const threeSupo = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];
  // 각 수포자가 몇점인지 체크
  const oneSupoScore = answers.filter((value, index) => { return value === oneSupo[index % oneSupo.length] }).length;
  const twoSupoScore = answers.filter((value, index) => { return value === twoSupo[index % twoSupo.length] }).length;
  const threeSupoScore = answers.filter((value, index) => { return value === threeSupo[index % threeSupo.length] }).length;

  // 최대 점수
  const maxScore = Math.max(oneSupoScore, twoSupoScore, threeSupoScore);

  if (oneSupoScore === maxScore) { answer.push(1) };
  if (twoSupoScore === maxScore) { answer.push(2) };
  if (threeSupoScore === maxScore) { answer.push(3) };

  return answer
}
```



## Comment

문제에서 제시된, 각 수포자들의 찍기 패턴을 배열의 형태로 선언해놓는다.

각 수포자의 점수를 구하기 위해서, `answers`의 요소와 찍기 패턴의 각 요소가 몇개 들어 맞는지 `filter`메소드로 구해낸다. 이때, `answers`의 `value`와 각 수포자들의 요소를 비교할 때, 수포자 배열 인덱스 접근을 `index % 각 배열.length`로 해야한다. `answser`의 인덱스가 수포자 배열의 길이보다 클 경우를 대비해서이다.

이후에는 `Math.max` 로 각 수포자 점수의 최댓값을 구해서 `if`문으로 최댓값과 같은 경우 `answer` 배열에 수포자 번호를 `push`한다.

## Reference

[프로그래머스](https://programmers.co.kr)

