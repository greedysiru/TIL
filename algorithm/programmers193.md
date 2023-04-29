

# [프로그래머스] 원소들의 곱과 합

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_list) => {
    // reduce로 모든 원소 들의 곱과 모든 원소들의 합의 제곱을 구하기
    const [acc1, acc2] = num_list.reduce((prev, cur) => {
        const [prevAcc1, prevAcc2] = prev;
        return [prevAcc1 * cur, prevAcc2 + cur];
    }, [1, 0]);
    // 모든 원소들의 곱과 모든 원소들의 합의 제곱을 비교하여 결과 반환
    return acc1 < acc2 ** 2 ? 1 : 0;
}
```

reduce를 활용하여 두 조건의 누적값을 배열의 형태로 return한다.

## Reference

[프로그래머스](https://programmers.co.kr)

