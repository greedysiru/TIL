# [프로그래머스] 구명보트 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 구명보트
from collections import deque

def solution(people, limit):
    answer = 0
    # 입력받은 사람의 몸무게를 오름차순으로 정렬
    people.sort()
    # deque 자료형으로 변환
    people = deque(people)
    # 구명보트의 개수를 세기
    # people이 빌때까지 진행
    while people:
        # 한 명만 남은 경우 보트를 보내고 반복문 중단
        if len(people) == 1:
            answer += 1
            break
        # 현재 남은 사람중에서 가장 가벼운 사람과 가장 무거운 사람이 보트에 탈 수 있는 지 검사
        if (people[0] + people[-1]) <= limit:
            # 가장 무거운 사람과 가장 가벼운 사람 people에서 빼기
            people.pop()
            people.popleft()
            # 보트수 +1
            answer += 1
        else:
            # 무게가 초과라면 가장 무거운 사람만 보트 태우기
            people.pop()
            # 보트수 +1
            answer += 1
    return answer
```



## Comment

deque를 활용하여 풀었다.

입력된 people 배열을 오름차순으로 정렬하면 해당 큐의 0번 인덱스에는 가장 가벼운 사람, -1번 인덱스에는 가장 무거운 사람이 있다. 반복문을 이용하여 ,매번 이 두 사람의 합이 무게 제한보다 낮다면, 두 사람을 태워 보낼 수 있으므로 보트 수를 +1 한다. 두 사람을 태워 보냈으므로 people은 popleft, pop 메소드를 사용해서 빼준다. 만약, 무게 제한보다 높다면, 무거운 사람만 보내도록하고 pop 메소드를 사용해서 빼준다.

# Reference

[프로그래머스](https://programmers.co.kr)

