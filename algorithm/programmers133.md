# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 1. 공 던지기

```JavaScript
const solution = (numbers, k) => numbers[(2 * (k - 1)) % (numbers.length)];
```



## 2. 진료 순서 정하기

```JavaScript
const solution = (emergency) =>  emergency.reduce((obj, item, index, origin) => {
    const {sortedEmergency, result} = obj;
    obj.result = [...result, sortedEmergency.indexOf(emergency[index]) + 1];
    return obj;
},{ sortedEmergency: emergency.slice().sort((a, b) => b - a), result: []}).result;
```



## 3. 외계어 사전

```JavaScript
const solution = (spell, dic) => dic.filter((word) => new RegExp(`(?=.*${spell.join(')(?=.*')})`, 'g').test(word)).length > 0? 1 : 2;
```



## 4. 문자열 밀기

```JavaScript
const solution = (A, B) => {
  let count = 0;
  let slicedString = A.slice();
  while (slicedString !== B) {
      count += 1;
      if (count === B.length) {
          count = -1;
          break;
      }
      slicedString = slicedString[slicedString.length - 1] + slicedString.slice(0, slicedString.length - 1);
  }
  return count;
};
```



## 5. 숨어있는 숫자의 덧셈(2)

```JavaScript
const solution = (my_string) => my_string.split(/[\D]+/g).reduce((acc, cur) => {
    if (cur !== '') {
        acc += Number(cur);
    }
    return acc;
}, 0);
```



## Reference

[프로그래머스](https://programmers.co.kr)

