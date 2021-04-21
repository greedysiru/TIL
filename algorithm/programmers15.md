# [프로그래머스] 나누어 떨어지는 숫자 배열 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 나누어 떨어지는 숫자 배열
def solution(arr, divisor):
    # divisor로 나누어 떨어지는 요소를 넣을 배열
    answer = []
    # arr을 하나씩 탐색하여 나누어 떨어지는 배열을 answer에 넣기
    for i in range(len(arr)):
        if arr[i] % divisor == 0:
            answer.append(arr[i])
    # answer 배열이 비어있는경우 -1을 넣기
    if len(answer) == 0:
        answer.append(-1)
    else:
        # 비어있지 않은 경우 오름차순 정렬
        answer.sort()
    return answer
```



## Comment

for문으로 하나씩 접근하며 나누었을 때 0이 되는 경우를 골라내면 된다.(if문)

# Reference

[프로그래머스](https://programmers.co.kr)

