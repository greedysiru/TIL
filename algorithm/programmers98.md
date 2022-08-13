# [프로그래머스] 신규 아이디 추천 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
function solution(new_id) {
    let convertedId = new_id
    // 1. 소문자로 치환
    .toLowerCase()
    // 2. 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자 제거
    .replace(/[^\w-_.]/g, '')
    // // 3. 마침표가 2번 이상 연속된 부분을 하나의 마침표로 치환
    .replace(/\.{2,}/g, '.')
    // // 4. 마침표가 처음이나 끝에 위치한다면, 제거
    .replace(/^\.|\.$/g, '')
    // // 5. 빈문자열이면 a를 대입
    .replace(/^$/, "a")
    // // 6. 15개의 문자를 제외한 나머지 문자들을 모두 제거
    .slice(0, 15)
    // // 6. 마침표가 끝에 위치하면 마침표 문자를 제거
    .replace(/\.$/, '')
    
    // 7. convertedId 길이가 2자 이하라면, 길이가 3이될 때 까지 마지막 문자를 반복해서 끝에 붙이기
    const lengthForconvertedId = convertedId.length;
    if (lengthForconvertedId <= 2) {
        // 마지막 문자
        const lastCharacterForconvertedId = convertedId[lengthForconvertedId - 1];
        while (convertedId.length < 3) {
            convertedId += lastCharacterForconvertedId;
        }
    }
    return convertedId;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

