

# [프로그래머스] n보다 커질 때까지 더하기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (numbers, n) => {
    let acc = 0;
    let index = 0;
    while (acc <= n) {
        acc += numbers[index];
        index += 1;
    }
    return acc;
}
```

1. 누적값을 저장할 변수 `acc` 를 선언 및 초기화
1. 순회할 `index`를 저장하는 변수 `index` 를 선언 및 초기화
1. `while`문 을 누적합이 n보다 작을 때만 실행하는 조건으로 실행



## Reference

[프로그래머스](https://programmers.co.kr)

