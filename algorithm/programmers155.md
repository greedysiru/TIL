# [프로그래머스] 푸드 파이트 대회 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드

```JavaScript
const solution = (foods) => {
    var answer = '';
    // 1. 수웅이가 준비한 음식을 순회하며, 홀수인 경우 -1(짝수화)
    // - foods[0]는 물이므로 생략
    const parsedFoods = 
          [...foods.slice(1).map((food) => food % 2 === 1? food - 1 : food)]
            // 2. 수웅이가 준비한 음식을 나열하기
            // - food는 수웅이가 준비한 음식의 수
            // - index + 1은 수웅이가 준비한 음식의 번호
            .map((food, index) => (index + 1).toString().repeat(food / 2))
            // 3. 0인 음식은 내지 못하므로 제거
            .filter(food => food !== 0);
    
    // 4. 답 return
    // - 왼쪽 선수가 먹을 음식을 나열한 배열인 parsedFoods를 문자열화
    // - 가운데에 0(물) 위치
    // - parsedFoods를 뒤집어서 오른쪽 선수가 먹을 음식을 나열한 배열로 바꾸고 문자열화
    return `${parsedFoods.join('')}0${parsedFoods.reverse().join('')}`
}
```



## Reference

[프로그래머스](https://programmers.co.kr)

