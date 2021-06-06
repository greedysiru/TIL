# [프로그래머스] JadenCase 문자열 만들기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# JadenCase 문자열 만들기
def solution(s):
    s_arr = s.split(' ')
    for i in range(len(s_arr)):
        s_arr[i] = s_arr[i].capitalize()
    return ' '.join(s_arr)
```



## Comment

capitalize 내상 함수로 간단하게 풀 수 있었다.

가장 첫 글자의 알파벳을 대문자로 바꿔주는 함수인데, 주어진 s를 split을 사용해서 공백을 기준으로 나눈 뒤, 만들어진 문자열 리스트의 원소를 하나씩 접근하여 capitalize를 하여 첫문자만 대문자로 바꿔주도록 하였다.

그 이후에는 join으로 공백을 기준으로 문자열을 생성하도록 하였다.

# Reference

[프로그래머스](https://programmers.co.kr)

