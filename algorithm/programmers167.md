

# [프로그래머스] 추억 점수 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (name, yearning, photo) => 
    photo
        // photo의 요소를 하나씩 접근하여 그리움 점수로 변환
        .map(p => p
                    // name에서 현재 접근한 인물의 몇 번째 인덱스에 있는지 찾고 yearning 배열에서의 점수를 더하기
                    // name에 없는 경우 0을 더하기
                    .reduce((acc, pName) => acc + (yearning[name.indexOf(pName)] || 0), 0))
```



## Reference

[프로그래머스](https://programmers.co.kr)

