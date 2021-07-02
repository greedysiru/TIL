# [프로그래머스] 카펫 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 카펫
function solution(brown, yellow) {
  let answer = [];
  // yellow, brown의 가로, 세로길이를 찾아내기
  let yellowWidth = 0;
  let yellowHeight = 0;
  for (let i = 1; i <= yellow; i++) {
    yellowWidth = i;
    if (yellow % yellowWidth > 0) {
      continue;
    }
    yellowHeight = yellow / yellowWidth;
    // borwn의 갯수가 맞는지 확인
    if ((((yellowWidth * 2) + 4) + (yellowHeight * 2)) === brown) {
      if (yellowWidth >= yellowHeight) {
        answer.push(yellowWidth + 2);
        answer.push(yellowHeight + 2);
        break;
      }
    }

  }
  return answer;
}
```



## Comment

 갈색 격자는 노란색 격자를 둘러 쌓는다. 예를 들어서, 노란색 격자가 가로 2, 세로 4로 이루어져 있다면 아래와 같다.

|   갈색   |    갈색    |    갈색    |   갈색   |
| :------: | :--------: | :--------: | :------: |
| **갈색** | **노란색** | **노란색** | **갈색** |
| **갈색** | **노란색** | **노란색** | **갈색** |
| **갈색** | **노란색** | **노란색** | **갈색** |
| **갈색** | **노란색** | **노란색** | **갈색** |
| **갈색** |  **갈색**  |  **갈색**  | **갈색** |

그러므로, 갈색 타일 갯수를 구하는 공식은 아래와 같다.

> **갈색 타일 갯수 = ((노란색 타일 가로  * 2) + 4) + (노란색 타일 세로 * 2)**

이 공식을 이용해서 `for문`으로 1부터 노란색타일의 갯수까지의 노란색 타일의 가로를 가정하며 노란색 타일의 세로를 구해내서 갈색 타일의 갯수를 계산해본다. 갈색 타일이 나오는 경우, 카펫의 가로 길이가 세로 길이 이상인 것을 염두해서 답을 구해야 한다.

## Reference

[프로그래머스](https://programmers.co.kr)

