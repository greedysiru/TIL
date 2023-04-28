

# [프로그래머스] 뒤에서 5등 위로

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_list) => num_list.sort((a, b) => a - b).slice(5)
```

주어진 배열을 오름차순으로 정렬 한 뒤, slice로 작은 5개 수를 제거한 새로운 배열을 반환할 수 있도록 함

## Reference

[프로그래머스](https://programmers.co.kr)

