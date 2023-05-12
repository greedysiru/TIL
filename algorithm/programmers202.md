

# [프로그래머스] 배열에서 문자열 대소문자 변환하기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (strArr) => strArr.map((str, index) => {
    // 인덱스가 짝수
    const isEven = index % 2 === 0;
    // 짝수인 경우는 소문자로, 홀수면 대문자로 변환
    return isEven? str.toLowerCase() : str.toUpperCase();
})
```



## Reference

[프로그래머스](https://programmers.co.kr)

