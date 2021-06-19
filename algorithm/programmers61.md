# [프로그래머스] 문자열 다루기 기본 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 문자열 다루기 기본
def solution(s):
    # 문자열의 길이가 4 혹은 6이고 숫자로만 이루어져 있을 때 True
    # 문자열의 길이
    s_len = len(s)
    if (s_len == 4 or s_len == 6) and s.isdigit():
        answer = True
    else:
        answer = False
    return answer
```



# Reference

[프로그래머스](https://programmers.co.kr)

