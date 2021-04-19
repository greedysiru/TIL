


# [프로그래머스] K번째 수 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# K번째 수
def solution(array, commands):
    answer = []
    # commands를 한 행씩 접근하여 슬라이싱하기
    for i in range(len(commands)):
        # 주어진 조건에 맞게 슬라이싱
        cut_array = array[commands[i][0] - 1:commands[i][1]]
        # 오름차순 정렬하기
        cut_array.sort()
        # 주어진 조건의 원소 꺼내어 답안 리스트 넣기
        answer.append(cut_array[commands[i][2] - 1])
    return answer
```



## Comment

주어진 2차원 리스트인 commands를 행 별로 접근해서 조건에 맞게 슬라이싱, 정렬, 특정 요소 빼기를 하면 되는 간단한 문제

# Reference

[프로그래머스](https://programmers.co.kr)

