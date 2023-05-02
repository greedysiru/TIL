

# [프로그래머스] my_string

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (rny_string) => rny_string.replaceAll('m', 'rn')
```

string built-in API인 replaceAll을 사용하여 문자열의 특정 부분 문자열을 대체할 수 있다.

replace를 사용한다면, 정규표현식을 사용해야 한다.

```JavaScript
const solution = (rny_string) => rny_string.replace(/m/g, 'rn')
```





## Reference

[프로그래머스](https://programmers.co.kr)

