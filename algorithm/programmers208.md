

# [프로그래머스] 문자열 곱하기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (my_string, k) => {
    let answer = '';
    for (let i = 0; i < k; i++) {
        answer += my_string;
    }
    return answer;
}
```

반복문을 사용한 일반적인 풀이이다.

사실 string API중 `repeat`을 사용하면 더 간결하고 간단하게 풀어낼 수 있다.

```JavaScript
const solution = (my_string, k) => my_string.repeat(k);
```





## Reference

[프로그래머스](https://programmers.co.kr)