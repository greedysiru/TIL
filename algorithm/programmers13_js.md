


# [프로그래머스] 베스트앨범 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 베스트앨범
function solution(genres, plays) {
  let answer = [];
  // genres 하나씩 접근
  // 장르별로 재생정보를 정리한 해시
  const genresPlaysHash = {};
  for (let i = 0; i < genres.length; i++) {
    // key초기화
    if (!(genres[i] in genresPlaysHash)) {
      // 0번 인덱스는 총 재생 횟수
      genresPlaysHash[genres[i]] = [['total', plays[i]]];
      // i번의 재생수
      genresPlaysHash[genres[i]].push([i, plays[i]]);
    }
    // key에 값 누적
    else {
      genresPlaysHash[genres[i]][0][1] += plays[i];
      genresPlaysHash[genres[i]].push([i, plays[i]]);
    }
  }
  // genresPlaysHash의 value로만 이루어진 배열 만들기
  const genresPlaysArray = Object.values(genresPlaysHash)
  // total 재생수를 기준으로 내림차순 정렬
  genresPlaysArray.sort((a, b) => b[0][1] - a[0][1]);
  // total 재생수가 많은 장르부터 하나씩 접근
  for (let genrePlaysInfo of genresPlaysArray) {
    // 각 장르별 음악을 재생수를 기준으로 내림차순 정렬
    genrePlaysInfo.sort((a, b) => b[1] - a[1]);
    // answer에 입력
    answer.push(genrePlaysInfo[1][0]);
    // 해당 장르가 한 곡밖에 없는 경우 아래의 코드를 실행하지 않기(하나만 입력하기)
    if (genrePlaysInfo.length === 2) {
      continue;
    }
    // 두 번째 곡 입력
    answer.push(genrePlaysInfo[2][0]);
  }
  return answer;
}
```



## Comment

장르별로 재생정보를 정리한 해시를 만든다. 해시의 `key`는 장르이며 `value`는 2차원 배열이며 장르의 총 재생수와 각 음악 번호 별 재생수가 입력되어 있다. 0번 인덱스는 `total` 또는 `음악 번호`이고 1번 인덱스는 재생수이다.

만들어진 해시를 재생수를 기준으로 정렬을 하기 위해서 `Object.values`를 사용해서 배열로 변환한다. 그 이후, `total`의 재생수를 기준으로 내림차순 정렬한다. 그 다음에는 `for 문`으로 각 요소를 접근해서 재생수 기준으로 내림차순 정렬하고 장르별로 앨범에 넣을 곡을 `answer`에 넣는다.



## Reference

[프로그래머스](https://programmers.co.kr)

