# [프로그래머스] 스킬트리 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 스킬트리
from collections import deque

def solution(skill, skill_trees):
    answer = 0
    # skill_trees를 하나씩 접근
    for skill_tree in skill_trees:
        # deque 변환
        skill_tree = deque(skill_tree)
        # skill을 deque 변환한 복사본을 넣기
        skill_clone = deque(skill)
        # skill_tree가 빌때까지 실행
        while skill_tree:
            # skill_tree의 가장 앞 요소 빼기
            skill_tree_first = skill_tree.popleft()
            # 가장 앞 요소가 skill_clone에 있는지 확인
            if skill_tree_first in skill_clone:
                # skill_clone의 가장 앞 요소와 같은지 확인
                # 같은 경우
                if skill_clone[0] == skill_tree_first:
                    # skill_clone 가장 앞요소 빼기
                    skill_clone.popleft()
                    # skill_clone이 비게되면 가능한 스킬트리
                    if not skill_clone:
                        answer += 1
                        break
                # 다른 경우
                elif skill_clone[0] != skill_tree_first:
                    # 불가능한 스킬트리이므로 break
                    break
        # 중단되지 않고 끝났다면 가능한 스킬트리
        else:
            answer += 1
    return answer
```



## Comment

`for`문을 사용해서 주어진 skill_trees를 하나씩 접근하여 `deque`로 변환하였다. 그리고 `while`문 안에서 `popleft()`메소드로 한 글자씩 접근하여 skill을 복사한 `deque`와 비교하였다. skill 복사본의 0번 인덱스와 같으면 선행 스킬을 만족하므로`popleft()`를 하여 skill 복사본의 가장 앞 요소를 제거하였다. 이때 skill 복사본이 비게된다면 카운트를 하고 `break`를 실행한다. 반면, 한 글자가 skill 복사본에 있으나 0번 인덱스에 있지 않다면 불가능한 스킬트리이므로 바로` break`를 하였다.` while`문을 `break`가 걸리지 않고 완료가 되었다면, 가능한 스킬트리이므로 카운트를 하였다.



# Reference

[프로그래머스](https://programmers.co.kr)