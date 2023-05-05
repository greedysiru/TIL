

# [프로그래머스] n개 간격의 원소들

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_list, n) => num_list.reduce((acc, cur, index) => index % n === 0? [...acc, cur] : acc , []);
```

새로운 배열을 만들어내는 것이므로 reduce를 활용했지만, filter가 있음을 간과하고 복잡하게 풀어낸 것 같다.

filter를 쓰면 아래와 같이 더 간단하게 풀어낼 수 있다.

```JavaScript
const solution = (num_list, n) => num_list.filter((_, index) => index % n === 0);
```





## Reference

[프로그래머스](https://programmers.co.kr)

