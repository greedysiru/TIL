# [프로그래머스] 전화번호 목록 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 전화번호 목록
def solution(phone_book):
    answer = True
    # phone_book의 해시를 기록할 딕셔너리
    phone_book_hash = {}
    # phone_book을 하나씩 접근하며 딕셔너리의 key로 기록
    for numbers in phone_book:
        phone_book_hash[numbers] = 1
    # phone_book_hash 기록 후 key 중에서 phone_book의 접두사가 되는 것이 있는 지 검사
    for numbers in phone_book:
        # 접두사가 있는지 체크할 문자열
        check = ''
        # 하나의 번호 문자열에서 딕셔너리에 key로 있는 지 검사
        for number in numbers:
            check += number
            # check가 딕셔너리의 Key로 있지만 번호와는 같지 않으면 접두사이므로 False
            if check in phone_book_hash and check != numbers:
                answer = False
    return answer
```



## Comment

해시에 대한 아이디어로 풀 수 있는 문제. 주어진 전화번호 목록을 딕셔너리의 key로 넣어 놓은 뒤, 전화번호를 하나씩 접근하며 일부의 숫자(문자열)가 해시의 key로 있는 지 그리고 전화번호와 다른 지를 검사한다.

# Reference

[프로그래머스](https://programmers.co.kr)

