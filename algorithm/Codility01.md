# [Codility] BinaryGap - JavaScript 풀이

**본 게시물은 Codility의 문제 풀이입니다.**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(number) {
    // 1. 주어진 수 2진수 변환
    const binaryNumber = number.toString(2);
    // 2. 1을 기준으로 잘라내기
    const slicedNumber = binaryNumber.slice(binaryNumber.indexOf('1'), binaryNumber.lastIndexOf('1'));   // 3. 1을 기준으로 배열로 나누기
    const convertedNumber = slicedNumber.split('1');
    console.log(convertedNumber);
    // 4. 길이가 가장 긴 요소가 최대 길이
    const longestBinaryGap = convertedNumber.reduce((gap, {length}) => length > gap? length : gap, 0);
    return longestBinaryGap;
}

```



## Reference

[Codility](https://app.codility.com/programmers/)

