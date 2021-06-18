# [프로그래머스] 문자열 내림차순으로 배치하기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 문자열 내림차순으로 배치하기
def solution(s):
    s = sorted(s, reverse=True)
    return ''.join(s)
```



## Comment

입력받은 문자열을 내림차순으로 배치하기 위해서 `sorted` 함수에 인자를 주어진 문자열과 `reverse=True`를 주어서 내림차순 정렬한다.

# Reference

[프로그래머스](https://programmers.co.kr)

