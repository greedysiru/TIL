
# [프로그래머스] 가운데 글자 가져오기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 가운데 글자 가져오기
def solution(s):
    # 글자의 길이
    s_length = len(s)
    # 글자의 길이가 홀수인 경우 가운데 글자를 뽑아내기
    if s_length % 2 == 1:
        answer = s[s_length // 2]
    # 글자의 길이가 짝수인 경우 가운데 두 글자를 뽑아내기
    if s_length % 2 == 0:
        answer = s[(s_length // 2) - 1:(s_length // 2) + 1]
    return answer
```



## Comment

홀수인 경우와 짝수인 경우 뽑아내는 글자의 조건이 다르므로 if문으로 분기처리해서 가운데 글자를 뽑아내면 된다. 슬라이싱을 할 때 인덱스의 숫자가 혼동스러울 수 있으니 주의. 테스트케이스를 찍어볼 것.

# Reference

[프로그래머스](https://programmers.co.kr)

