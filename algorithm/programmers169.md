

# [프로그래머스] 둘만의 암호 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (s, skip, index) => {
    var answer = '';
    // a의 ASCII code
    const A_ASCII = 'a'.charCodeAt(0);
    // z의 ASCII code
    const Z_ASCII = 'z'.charCodeAt(0);
    // skip할 문자열들의 ASCII code
    const skipASCIIs = skip.split('').map((s) => s.charCodeAt(0));
    const convertedS = s
                        // 배열로 변환
                        .split('')
                        .map((str) => {
                            // index 만큼 이동시키기
                            // 이동 수를 셀 변수
                            let count = 0;
                            // str의 ASCII
                            let strASCII = str.charCodeAt(0);
                            // count가 index와 같아지면 중단
                            while (count < index) {
                                // z를 넘으면 a부터 시작
                                if (strASCII + 1 > Z_ASCII) {
                                    strASCII = A_ASCII;
                                } else {
                                    // 아닌 경우 다음 
                                    strASCII += 1;
                                }
                                // skip이 아닌 경우에만 count
                                if (!skipASCIIs.includes(strASCII)) {
                                    count += 1;
                                }
                            }
                            // strASCII를 문자열로 변환
                            return String.fromCharCode(strASCII);
                        })
                        // 문자열로 변환
                        .join('');
    return convertedS;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

