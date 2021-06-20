# [프로그래머스] 콜라츠 추측 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 콜라츠 추측
def solution(num):
    # 카운트가 500 미만일 때까지 반복
    # 카운트
    count = 0
    while count < 500:
        # num이 1이되면 반복 중단
        if num == 1:
            break
        # num을 2로 나누었을 때의 나머지
        num_remainder = num % 2
        # 짝수인 경우
        if num_remainder == 0:
            # 2로 나누기
            num /= 2
            # 카운트
            count += 1
        # 홀수인 경우
        elif num_remainder == 1:
            # 3으로 곱한 뒤 1을 더하기
            num = (num * 3) + 1
            count += 1
    # count가 500이 될 때까지 num이 1이 되지 않으면 -1을 출력
    else:
        count = -1
    return count
```



## Comment

num이 짝수인지 홀수인지를 판별하기 위해서는 모듈러 연산(%)을 사용하여 0일 때는 짝수처리 1일때는 홀수처리를 한다. 문제에서 해당 작업을 500번 반복해도 1이 되지 않으면 -1을 출력하라고 했으므로,` while`문의 실행 조건을 500미만으로 한다. 그리고 이 반복문안에서 num이 1이 되면` break`로 중단하고 500번이 되었을 때도 1이 안나왔을 때는 `while`의` else`가 실행되므로 -1을 출력하도록 한다.



# Reference

[프로그래머스](https://programmers.co.kr)