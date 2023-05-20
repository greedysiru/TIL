

# [프로그래머스] 이어 붙인 수

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (숫자들) => {
    const 홀수와짝수들 = 숫자들.reduce((홀수짝수, 숫자) => {
        숫자 % 2 === 0? 홀수짝수['짝수'] += 숫자.toString() : 홀수짝수['홀수'] += 숫자.toString();
        return 홀수짝수;
    }, {'홀수': '', '짝수': ''});
    return Object.values(홀수와짝수들).reduce((합, 문자열화된숫자) => 합 += parseInt(문자열화된숫자), 0);
}
```

이번엔 변수명을 한글로 해보았다.



## Reference

[프로그래머스](https://programmers.co.kr)

