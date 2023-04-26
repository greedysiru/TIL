

# [프로그래머스] 문자열 뒤의 n글자

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (my_string, n) => my_string.slice(my_string.length - n)
```

문자열의 slice API는 전달받은 매개변수에 따라 문자열을 잘라내 반환한다.

문제에서는 문자열 뒤의 n글자를 필요로 하였는데, 문자열 끝으로부터 n번째에 해당하는 문자열 Index를 구하면 된다. 아래와 같이 계산하면 해당 Index를 구할 수 있다.

> '대상 문자열'.length - n

## Reference

[프로그래머스](https://programmers.co.kr)

