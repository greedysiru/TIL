# [프로그래머스] 문자열 내 p와 y의 개수 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 문자열 내 p와 y의 개수
def solution(s):
    # 주어진 문자열을 대문자로 통일
    s = s.upper()
    # p를 카운트할 변수
    p_count = 0
    # y를 카운트할 변수
    y_count = 0
    # 주어진 문자열 탐색
    for i in range(len(s)):
        # p 카운트
        if s[i] == 'P':
            p_count += 1
        elif s[i] == 'Y':
            y_count += 1
    # 탐색 후 p, y 가 같은경우
    if p_count == y_count:
        return True
    # 다른 경우
    elif p_count != y_count:
        return False
```



## Comment

문자열 전체를 대문자나 소문자로 변환하여 for문으로 하나씩 접근했을 때 p, y가 나오게 되면 카운트를 하는 if문을 작성한다. 탐색후 p,y의 개수가 같거나 0인 경우와 다른 경우를 True, False로 반환한다.

# Reference

[프로그래머스](https://programmers.co.kr)

