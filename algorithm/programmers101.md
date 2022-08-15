# [프로그래머스]  뉴스 클러스터링 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```JavaScript
// 자카드 유사도를 구하는 함수
function getJaccardCoefficient(a, b) {
    // 모든 집합이 공집합이면 1을 return
    if(a.length === 0 && b.length === 0) {
        return 65536;
    }
    // 두 집합의 단순 병합
    const merged = [...a, ...b];
    // 두 집합의 교집합
    const intersection = [];
    for (let bElement of b) {
        if (a.includes(bElement)) {
            a.splice(a.indexOf(bElement), 1);
            intersection.push(bElement);
        }
    }
    // 자카드 유사도 return
    // 다중집합 합집합 = 병합 - 교집합
    return parseInt((intersection.length / (merged.length - intersection.length)) * 65536);
}

// 두 글자씩 끊어서 다중집합 원소로 만드는 함수
function makeMultipleSets(str1, str2) {
    // 두 문자 모두 대문자화
    const convertedStr1 = str1.toUpperCase();
    const convertedStr2 = str2.toUpperCase();
    // 다중집합을 담을 배열
    const multipleSet1 = [];
    const multipleSet2 = [];
    // 각 문자열을 순회하며 다중집합 만들기
    for (let i = 0; i < convertedStr1.length - 1; i++) {
        // 두개씩 끊어서 만들기
        const parsedString = convertedStr1.slice(i, i + 2).trim().replace(/[^A-Z]/g, '');
        if (parsedString.length === 2) {
            multipleSet1.push(parsedString);
        }
    }
    for (let j = 0; j < convertedStr2.length - 1; j++) {
        // 두개씩 끊어서 만들기
        const parsedString = convertedStr2.slice(j, j + 2).trim().replace(/[^A-Z]/g, '');
        if (parsedString.length === 2) {
            multipleSet2.push(parsedString);
        }
    }
    // 만든 집합을 return
    return [multipleSet1, multipleSet2];
}

function solution(str1, str2) {
    const [set1, set2] = makeMultipleSets(str1, str2);
    const jaccardCoefficient = getJaccardCoefficient(set1, set2);
    return jaccardCoefficient;
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

