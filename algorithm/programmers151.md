# [프로그래머스] 다항식 더하기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (polynomial) => {
    const parsedPolynomial = polynomial.split('+').reduce((arr, cur) => {
    let [xNumber, commonNumber] = arr;
    cur.trim();
    if (cur.includes('x')) {
        const removedX = Number(cur.replace('x', ''));
        xNumber += removedX !== 0? removedX : 1;
    } else {
        commonNumber += Number(cur);
    }
    return [xNumber, commonNumber];
}, [0, 0]);
    return parsedPolynomial.map((number, index) => {
        if (index === 0) {
            if (number < 10) {
                number = number.toString().replace('1', '');
            } 
            return number != 0 || number === '' ? `${number}x`: null;
        } else if (index === 1){
            return number !== 0? number : null ;
        }
    }).filter((number) => number !== null).join(' + ');
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

