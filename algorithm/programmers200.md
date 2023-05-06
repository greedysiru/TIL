

# [프로그래머스] 조건에 맞게 수열 변환하기 1

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (arr) => arr.map((num) => {
    if (num >= 50 && num % 2 === 0) return num / 2;
    if (num < 50 && num % 2 === 1) return num * 2;
    return num;
})
```

map API를 사용해서 각 조건에 해당하는 값을 return하도록 분기처리 한다.



## Reference

[프로그래머스](https://programmers.co.kr)

