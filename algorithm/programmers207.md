

# [프로그래머스] 카운트다운

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (start, end) => Array.from({length: start - end + 1}, (_, index) => start - index );
```

`Array.from` 을 사용하여 첫번째 파라미터에는 필요한 길이만큼의 length를 넘기고(유사 배열), 두번쨰 파라미터에는 콜백으로 각 요소를 동적 생성하도록 하였다.



## Reference

[프로그래머스](https://programmers.co.kr)

