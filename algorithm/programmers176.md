

# [프로그래머스] 뒤에서 5등 위로 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_list) => num_list.findIndex(num => num < 0);
```

num_list는 배열로 들어온다. 그리고 첫 번째로 나오는 음수를 구해야한다.

findIndex는 전달받은 콜백 함수의 결과가 true인 첫 번째 요소의 인덱스를 return하므로 해당 API를 사용하여 해결했다.



## Reference

[프로그래머스](https://programmers.co.kr)

