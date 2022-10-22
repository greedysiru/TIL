# [프로그래머스] 코딩테스트 입문 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 1. 2차원으로 만들기

```JavaScript
const solution = (num_list, n) => num_list.reduce((array, number, index) => {
    const arrayIndex = Math.floor(index / n);
    if (array[arrayIndex] === undefined) {
        array[arrayIndex] = [number];
    } else {
        array[arrayIndex].push(number);
    }
    return array;
}, [])
```



## 2. 한 번만 등장한 문자

```JavaScript
const solution = (s) => s.split('').sort().reduce((result, string, _, originS) => {
    const filteredS = originS.filter(item => item === string);
    if (filteredS.length === 1) {
        result += string;    
    }
    return result;
}, '');
```



## 3. 종이 자르기

```JavaScript
const solution = (M, N) => (M - 1) + (M * (N - 1));
```



## 4. 모스부호(1)

```JavaScript
const morse = { 
    '.-':'a','-...':'b','-.-.':'c','-..':'d','.':'e','..-.':'f',
    '--.':'g','....':'h','..':'i','.---':'j','-.-':'k','.-..':'l',
    '--':'m','-.':'n','---':'o','.--.':'p','--.-':'q','.-.':'r',
    '...':'s','-':'t','..-':'u','...-':'v','.--':'w','-..-':'x',
    '-.--':'y','--..':'z'
};

const solution = (letter) => letter.split(' ').reduce((obj, string) => {
    let {accString, result} = obj;
    accString += string;
    if (Object.keys(morse).includes(accString)) {
        obj.result += morse[accString];
        obj.accString = '';
    } else {
        obj.accString = accString;
    }
    return obj;
}, {accString: '', result: ''}).result;
```



## 5. 이진수 더하기

```JavaScript
const solution = (bin1, bin2) => (parseInt(bin1, 2) + parseInt(bin2, 2)).toString(2);
```





## Reference

[프로그래머스](https://programmers.co.kr)

