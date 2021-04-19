


# [프로그래머스] 2016년 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 2016년
def solution(a, b):
    # 진행된 일수
    date = 0
    # a월 1일까지의 일수 구하기
    for i in range(1, a):
        # i가 7이하일 때
        if i <= 7:
            # 2월이면 29일(윤년)
            if i == 2:
                date += 29
                continue
            # 홀수이면 31일
            if i % 2 == 1:
                date += 31
                continue
            # 짝수이면 30일
            elif i % 2 == 0:
                date += 30
                continue
        # i가 8이상일 때
        elif i >= 8:
            # 홀수이면 30일
            if i % 2 == 1:
                date += 30
                continue
            # 짝수이면 31일
            elif i % 2 == 0:
                date += 31
                continue
    # 주어진 일수 b를 date에 더하기
    date += b
    # 주어진 일수를 1을 빼고 7을 나눈 나머지를 요일에 넣는다
    day = (date - 1) % 7
    # 2016.1.1이 금요일이므로 if문으로 적절한 요일을 answer에 넣기
    # 0이면 일주일 지난것과 같으므로 이것을 기준으로 지난 일수에 따른 요일 적용
    if day == 0:
        answer = "FRI"
    elif day == 1:
        answer = "SAT"
    elif day == 2:
        answer = "SUN"
    elif day == 3:
        answer = "MON"
    elif day == 4:
        answer = "TUE"
    elif day == 5:
        answer = "WED"
    elif day == 6:
        answer = "THU"
    return answer
```



## Comment

문제에서 2016년이 윤달이라고 적혀있다. 이를 고려해서 if문으로 주어진 달의 1일까지 구한 후 모듈러 연산으로 남게되는 수를 기준으로 요일을 출력하면 된다.

# Reference

[프로그래머스](https://programmers.co.kr)

