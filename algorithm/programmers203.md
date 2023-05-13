

# [프로그래머스] 글자 이어 붙여 문자열 만들기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (my_string, index_list) => index_list.reduce((str, index) => `${str}${my_string[index]}`, '');
```

reduce를 사용하여, 이어붙인 문자열을 만들어 낸다. 이 때 초기값을 빈 문자열을 전달한다. 그렇지 않으면 index_list의 첫 요소를 넣게 된다.



## Reference

[프로그래머스](https://programmers.co.kr)

