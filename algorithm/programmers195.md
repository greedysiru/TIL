

# [프로그래머스] 배열 만들기 1

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (n, k) => {
    const answer = [];
    // n이하의 정수 중 k의 배수 개수
    const multipleEa = parseInt(n / k);
    // k의 배수 개수만큼의 길이를 가지는 Array Like를 전달
    // index + 1하여 * k를 하도록 콜백을 전달
    return Array.from({length : multipleEa}, (_, index) => k * (index + 1));
}
```

Array의 built-in API의 from을 활용하면, 유연하고 확장성 있게 배열을 생성해 낼 수 있다.

첫 번째 인자로 length 프로퍼티를 가지고 있는 유사 배열을 전달하면, 그 길이만큼의 빈 배열이 생성되고 두 번째 인자의 콜백을 생성된 요소를 순회하며 실행한다. 이 때, 콜백의 첫 번째 인자는 접근한 요소이고 두 번째 인자는 인덱스인 것을 기억하여 활용한다.

## Reference

[프로그래머스](https://programmers.co.kr)

