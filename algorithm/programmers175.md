

# [프로그래머스] 달리기 경주 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (players, callings) => {
    // 등수: 선수인 object, 선수: 등수인 object로 변환
    const [obj1, obj2] = players.reduce((acc, cur, index) => {
        const [obj1, obj2] = acc;
        obj1[index + 1] = cur;
        obj2[cur] = index + 1;
        return [obj1, obj2];
    }, [{}, {}]);
    // 최종 결과 구하기
    callings.forEach((cur) => {
        // 불린 선수의 등수
        const curRank = obj2[cur];
        // 불린 선수 앞에 있는 선수
        const fasterPlayer = obj1[curRank - 1];
        // obj1, obj2 최신화하기
        obj1[curRank - 1] = cur;
        obj1[curRank] = fasterPlayer;
        obj2[fasterPlayer] = curRank;
        obj2[cur] = curRank - 1;
    });
    return Object.values(obj1);
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

