

# [프로그래머스] n 번째 원소부터

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_list, n) => num_list.slice(n - 1);
```

n 번째 부터 원소를 자르는 것이므로 Array API인 slice를 사용한다. 단, slice는 전달 받은 수 다음의 인덱스부터 잘라내므로 n - 1을 전달해야함에 유의한다.



## Reference

[프로그래머스](https://programmers.co.kr)

