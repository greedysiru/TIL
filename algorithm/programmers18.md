# [프로그래머스] 문자열 내 마음대로 정하기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 문자열 내 마음대로 정하기
def solution(strings, n):
    answer = sorted(strings, key=lambda x: (x[n], x))
    return answer
```



## Comment

람다식을 참고하여 풀었다.

# Reference

[프로그래머스](https://programmers.co.kr)

