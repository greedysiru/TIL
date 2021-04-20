
# [프로그래머스] 같은 숫자는 싫어 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 같은 숫자는 싫어
def solution(arr):
    # 답을 담을 배열
    answer = []
    # 주어진 배열을 하나씩 접근
    for i in range(len(arr)):
        # 처음 인덱스면 무조건 넣기
        if i == 0:
            answer.append(arr[i])
        # i가 1 이상일 때 이 전에 들어간 원소가 같지 않을 때만 넣기
        if i >= 1:
            if arr[i - 1] != arr[i]:
                answer.append(arr[i])

    return answer
```



## Comment

간단하다. 처음인 경우만 예외처리를 하고 그 이후는 이전의 인덱스의 원소가 같지 않을 때만 답안 리스트에 들어가도록 하면 된다.

# Reference

[프로그래머스](https://programmers.co.kr)

