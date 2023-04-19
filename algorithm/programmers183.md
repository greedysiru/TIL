

# [프로그래머스] 문자열 정수의 합

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (num_str) => num_str.split('').reduce((acc, cur) => acc + parseInt(cur) , 0);
```

1. 전달받은 num_str을 split('')으로 배열로 나눔
2. 배열의 각 누적합을 구하기
   * 첫 번째 파라미터 콜백에서 누적합을 실행할 함수 전달
   * 두 번째 파라미터에는 누적합을 시작하기 전 초기값
   * num_str을 배열로 변환하여도 각 요소는 string이므로 parseInt로 정수 값으로 변환



## Reference

[프로그래머스](https://programmers.co.kr)

