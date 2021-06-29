


# [프로그래머스] 프린터 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 프린터
function solution(priorities, location) {
  let answer = 0;
  // priorities에서 목표 문서를 표시하는 배열 생성
  const checkArray = [];
  // 목표 문서의 위치 요소는 true, 나머지는 false로 초기화
  for (let i = 0; i < priorities.length; i++) {
    if (i === location) {
      checkArray[i] = true;
    } else {
      checkArray[i] = false;
    }
  }
  // priorites가 전부 비워질 때까지 실행
  while (priorities.length > 0) {
    // priorites와 checkArray 첫 요소를 가져오기
    const firstPriority = priorities.shift();
    const firstCheck = checkArray.shift();
    // 해당 요소보다 큰 요소가 있는지 없는지를 판별할 변수
    let flag = true;
    for (let j = 0; j < priorities.length; j++) {
      if (firstPriority < priorities[j]) {
        // 뒤로 넘기기
        priorities.push(firstPriority);
        checkArray.push(firstCheck);
        // 큰 요소가 있으므로 false
        flag = false;
        break
      }
    }
    // flag가 true이면 가장 중요한 문서이므로 출력처리
    if (flag) {
      answer += 1;
      // 목표로한 문서인 경우 중단
      if (firstCheck) {
        break
      }
    }
  }
  return answer;
}
```



## Comment

목표로 하는 문서의 위치를 판별하기 위해서, 별도의 `checkArray`를 만든다. 목표로하는 인덱스는 `ture`로 초기화 하도록 한다. 

주어진 `priorities`가 비어질 때까지 `while`을 반복한다. 이때, `priorites`와 `checkArray`의 가장 맨 앞 요소를 `shift`를 통해서 가져오고 해당 요소보다 큰 요소가 있는 지 없는 지를 판별하는 불린 변수 `flag`를 `true`로 선언한다. 

`for문`을 통해서 `priorities` 의 맨 앞 요소와 다른 요소를 비교한다. 큰 요소가 있는 경우 `priorities`, `checkArray` 맨 앞 요소를 `push`로 다시 원래 배열의 뒤로 넣는다. 그리고 `flag`를 `false`로 초기화하고 `break`하여 반복문을 중단한다.

만약, 큰 요소가 없는 경우 `flag`가 `true`이므로 `if문`을 통해서 몇 번째 문서인지 기록하고 가져온 `checkArray`의 첫 요소가 `true`이면 `break`로 완료 처리한다.



## 모범 코드

```JavaScript
function solution(priorities, location) {
    var list = priorities.map((t,i)=>({
        my : i === location,
        val : t
    }));
    var count = 0;        
    while(true){
        var cur = list.splice(0,1)[0];        
        if(list.some(t=> t.val > cur.val )){
            list.push(cur);                        
        }
        else{            
            count++;
            if(cur.my) return count;
        }
    }
}
```



## Comment

`map, some` 메소드를 통해서 가독성이 좋고 효율적인 코드를 작성하는 답안. ES5+ 이후 문법도 활용하는 습관을 가져야 겠다.

## Reference

[프로그래머스](https://programmers.co.kr)

