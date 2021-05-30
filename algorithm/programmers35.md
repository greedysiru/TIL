# [프로그래머스] 최댓값과 최솟값 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 최댓값과 최솟값
def solution(s):
    # 공백을 기준으로 나누어 숫자 입력
    numbers = s.split(' ')
    # 최솟값과 최댓값 구하기
    max_num = -int(1e9)
    min_num = int(1e9)
    # 반복문으로 하나씩 탐색
    for i in range(len(numbers)):
        num = int(numbers[i])
        if num > max_num:
            max_num = num
        if num < min_num:
            min_num = num
    answer = str(min_num) + ' ' + str(max_num)
    return answer
```



## Comment

매우 간단한 문제. split 메소드와 map을 사용하여 더 짧은 코드를 작성할 수 있다.

```python
def solution(s):
    s = list(map(int,s.split()))
    return str(min(s)) + " " + str(max(s))
```

# Reference

[프로그래머스](https://programmers.co.kr)

