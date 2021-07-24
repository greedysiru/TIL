# [프로그래머스] 약수의 개수와 덧셈 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 약수의 개수와 덧셈
# 약수를 세는 함수
def count_measure(number):
    count = 0
    for j in range(1, number):
        if number % j == 0:
            count += 1
    return count


def solution(left, right):
    answer = 0
    # 약수 구하기
    for i in range(left, right + 1):
        # 약수의 개수
        count = count_measure(i)
        # 짝수인 경우 더하기
        if count % 2:
            answer += i
            print(i)
        #  홀수이면 빼기
        else:
            answer -= i
            print(i)
    return answer
```



# Reference

[프로그래머스](https://programmers.co.kr)

