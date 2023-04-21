

# [프로그래머스] 카운트 업

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (start, end) => Array.from({length: end - start + 1}, (_, i) => start + i);
```

Array.from()은 유사 배열 객체를 얕게 복사하여 새로운 배열을 생성해낸다. 또 두 번째 매개변수로 콜백을 전달하여 각 배열 요소에 대해  해당 함수를 호출할 수 있다.(optional)

1.  end - start + 1 하여 만들 숫자 리스트만큼의 수 만큼의 length를 가지는 객체 리터럴을 전달
2. 콜백 함수에서는 index를 start에 순차적으로 더하기



## Reference

[프로그래머스](https://programmers.co.kr)

