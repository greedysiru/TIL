# [프로그래머스] 완주하지 못한 선수 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 완주하지 못한 선수
def solution(participant, completion):
    # 똑같은 순서가 오도록 정렬
    participant.sort()
    completion.sort()
    # 완주자 리스트 길이만큼 탐색
    for i in range(len(completion)):
        # 완주자 길이만큼 탐색시 같지 않은 선수는 완주하지 못한 선수
        if participant[i] != completion[i]:
            return participant[i]
    # 탐색이 무사히 끝났다면 participant의 마지막 요소가 완주하지 못한 선수
    return participant.pop()
```



## Comment

참가자 리스트와 완주자 리스트를 각각 정렬을 한 뒤 for문으로 완주자 리스트 만큼 탐색하면, 탐색과정에서 다른 것이 나오면 그것이 답이다(중복 참가자인 경우) 탐색 과정이 return 되지 않고 끝났으면 참가자  리스트의 마지막 요소가 답이된다.

# Reference

[프로그래머스](https://programmers.co.kr)

