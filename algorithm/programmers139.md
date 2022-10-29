# [프로그래머스]  로그인 성공? - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (id_pw, db) => {
    const [id, pw] = id_pw;
    const idPwPairTable = db.reduce((idPwPairTable, idPwPair) => {
        idPwPairTable[idPwPair[0]] = idPwPair[1];
        return idPwPairTable;
        }, {})
    if (idPwPairTable[id] === pw) {
        return "login";
    } else if (idPwPairTable[id] === undefined) {
        return 'fail'
    } else if (idPwPairTable[id] !== pw){
        return "wrong pw";
    }
};
```



## Reference

[프로그래머스](https://programmers.co.kr)

