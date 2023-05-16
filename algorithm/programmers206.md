

# [프로그래머스] 특정한 문자를 대문자로 바꾸기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (my_string, alp) => my_string.replace(new RegExp(alp, 'g'), alp.toUpperCase());
```

`replace`를 활용하였다.

첫번째 파라미터는 `바꿀 문자열` 또는 `정규 표현식`을 넣어주면되는데, 문제의 조건 상 동적으로 `정규 표현식`을 생성해서 넣어주는 것이 효율적이다. 그래서 `RegExp` 을 활용하여 `alp`에 해당하는 정규표현식을 동적 생성하도록 했다. 두번째 파라미터는 `alp`를 대문자화한 문자열을 넣어주도록 하였다.

replace말고 replaceAll을 활용할 경우 아래와 같이 하면 된다.

```JavaScript
const solution = (my_string, alp) => my_string.replaceAll(alp, alp.toUpperCase());
```





## Reference

[프로그래머스](https://programmers.co.kr)

