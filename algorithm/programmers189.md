

# [프로그래머스] n 번째 원소까지

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_list, n) => num_list.slice(0, n);
```

배열의 slice API는 첫번째로 전달받은 파라미터(index)로부터 두번째로 전달받은 파라미터 - 1(index)까지 배열을 잘라낸 얕은 복사본을 반환한다.

## Reference

[프로그래머스](https://programmers.co.kr)

