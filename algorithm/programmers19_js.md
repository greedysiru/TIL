# [프로그래머스] H-Index - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// H-Index
function solution(citations) {
  let answer = 0;
  // 오름차순 정렬
  citations.sort((a, b) => a - b);
  console.log(citations)
  // 정렬한 배열을 하나씩 접근
  for (let i = 0; i < citations.length; i++) {
    // 주어진 논문의 인용된 횟수
    const citation = citations[i];
    // 인용 횟수
    const citationCount = citations.length - i;
    console.log(citation, citationCount)
    if (citation >= citationCount) {
      answer = (answer < citationCount ? citationCount : answer);
    }
  }
  return answer;
}
```



## Comment

주어진 `citations`를 오름차순 정렬하고 하나씩 접근 한다. 이때 H-index의 인용횟수는 배열을 참조하는 것이 아니라 별개이다. 반복문에서 최대로 인용될 수 있는 횟수(`citations.length`)로부터 하나씩 빼며 이 횟수보다 인용횟수가 이상일 때, `answer`에 최댓값을 최신화 한다.

> **[0, 1, 20, 40, 41]**

즉 위의 경우에서, 20, 40, 41은 인용횟수가 3번 이상이므로 3이 H-Index이다.

문제의 로직 자체는 어렵지 않은데 독해력이 많이 요구되는 문제였던 것 같다.

## Reference

[프로그래머스](https://programmers.co.kr)

