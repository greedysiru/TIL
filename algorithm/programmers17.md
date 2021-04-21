# [프로그래머스] 폰켓몬 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 폰켓몬
def solution(nums):
    answer = 0
    # nums의 길이 반이 고를 수 있는 폰켓몬의 수
    pick = len(nums) / 2
    # nums를 집합 자료형 변환하여 중복 제거후 다시 리스트 변환
    nums = list(set(nums))
    # 중복을 제거한 nums의 길이가 pick과 크거나 같으면 가질 수 있는 최대 종류는 pick과 같다.
    if len(nums) >= pick:
        answer = pick
    # nums의 길이가 작은 경우 그 만큼의 종류를 가질 수 있다.
    elif len(nums) < pick:
        answer = len(nums)
    return answer
```



## Comment

set으로 중복을 제거하고 if문으로 분기하여 답을 도출해냈다. 중복이 제거되었을 때, 폰켓몬 리스트가 뽑을 수 있는 수보다 크거나 작으면 뽑을 수 있는 수가 답이되는 것이고 폰켓몬 리스트가 뽑을 수 있는 수보다 작으면 폰켓몬 리스트의 길이가 답이다.

# Reference

[프로그래머스](https://programmers.co.kr)

