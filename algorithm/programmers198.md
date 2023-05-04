

# [프로그래머스] 길이에 따른 연산

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_list) => num_list.reduce(num_list.length >= 11? (acc, cur) => acc + cur : (acc, cur) => acc * cur);
```

요소를 순회하여 연산 후 누적된 값을 return해야한다. 연산에 대한 콜백을 삼항 연산자로 조건에 맞게 전달한다.



## Reference

[프로그래머스](https://programmers.co.kr)

