# [프로그래머스] 짝지어 제거하기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 짝지어 제거하기
def solution(s):
    # 짝지어진 문자를 검사할 check 리스트
    check = []
    # s의 문자열 하나씩 접근
    for x in s:
        # check가 비어있는 경우 문자 넣기
        if not check:
            check.append(x)
        # check에 마지막으로 들어온 문자가 현재 접근한 문자와 같은경우 pop(짝이 맞는 경우)
        elif check[-1] == x:
            check.pop()
        # 짝이 맞지 않는경우 현재 문자를 넣기
        else:
            check.append(x)
    # 모든 문자열을 검사후 check가 비어있으면 1, 비어있지 않으면 0
    if not check:
        answer = 1
    else:
        answer = 0
    return answer
```



## Comment

문자열의 연속한 문자가 짝지어져 있는 지 검사하기 위해서 별도의 리스트 check를 만들고 for문으로 하나씩 문자를 검사하였다. check가 비어있으면 현재 문자를 넣고, 문자가 있는 경우 가장 마지막에 들어온 문자와 현재 접근한 문자를 비교하여 짝지어짐 여부를 판별하였다. 짝지어져있으면 check 리스트에서 pop처리하면 된다.

# Reference

[프로그래머스](https://programmers.co.kr)