

# [프로그래머스] 배열 비교하기

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드



```JavaScript
const solution = (배열1, 배열2) =>  {
    const 배열1길이 = 배열1.length;
    const 배열2길이 = 배열2.length;
    if (배열1길이 > 배열2길이) return 1;
    if (배열1길이 < 배열2길이) return -1;
    if (배열1길이 === 배열2길이) {
        const 배열1모든원소합 = 배열1.reduce((acc, cur) => acc + cur);
        const 배열2모든원소합 = 배열2.reduce((acc, cur) => acc + cur);
        if (배열1모든원소합 > 배열2모든원소합) return 1;
        if (배열1모든원소합 < 배열2모든원소합) return -1;
        if (배열1모든원소합 === 배열2모든원소합) return 0;
    }
    return answer;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

