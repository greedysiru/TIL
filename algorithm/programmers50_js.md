# [프로그래머스] 신고 결과 받기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 자바스크립트 코드(나의 풀이)

```javascript
function solution(id_list, report, k) {
    const answer = [];
    // id별 신고한 id를 기록하는 object 초기화
    const idReportedObject = {};
    for (const id of id_list) {
        idReportedObject[id] = [];
        answer.push(0);
    }
    
    // rerport 배열 순회
    for (const rep of report) {
        // split로 공백 기준으로 쪼개기
        // 0번 인덱스는 신고하는 id, 1번 인덱스는 신고당한 id
        const [reportId, reportedId] = rep.split(' ');
        // 기록하기
        // 중복 신고는 무시
        if (!idReportedObject[reportedId].includes(reportId)) {
            idReportedObject[reportedId].push(reportId)
        }
    }
    // 메일 보내기
    for (const id of id_list){
        // k이상 신고 받은 경우
        if (idReportedObject[id].length >= k) {
            for (const sendForId of idReportedObject[id]) {
                answer[id_list.indexOf(sendForId)] += 1;
            }
        }
    }

    return answer;
}
```

자꾸 파이프라인을 까먹는데 습관이 안되어 있다. 알고리즘을 종종 풀면서 습관이 되도록 하자.

## Reference

[프로그래머스](https://programmers.co.kr)

