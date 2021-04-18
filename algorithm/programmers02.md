


# [프로그래머스] 신규 아이디 추천 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 신규 아이디 추천
def solution(new_id):
    # 아이디를 조건에 맞게 변경하기
    # 아이디에 허용되는 문자열들
    is_able = ['-', '_', '.']
    # 대문자를 소문자로 변환
    new_id = new_id.lower()
    # 아이디의 길이
    id_length = len(new_id)
    # 규칙에 맞는 아이디
    available_id = []
    # 한 글자씩 접근
    for i in range(id_length):
        #  숫자거나 허용된 문자열인 경우에만 새 아이디에 넣기
        if (new_id[i].isdigit() or new_id[i] in is_able or new_id[i].isalpha()):
            available_id.append(new_id[i])
            # 현재 규칙에 맞는 아이디의 길이
            # 마침표가 두 번 연속한 경우 하나 제거
            if len(available_id) >= 2:
                if available_id[-1] == '.' and available_id[-2] == '.':
                    available_id.pop()

      # 마침표가 처음에 있으면 제거
    if available_id[0] == '.':
        available_id.pop(0)

    if len(available_id) >= 1:
        #  마침표가 마지막에 있으면 제거
        if available_id[-1] == '.':
            available_id.pop()

    # 빈 문자열이면 a를 대입
    if len(available_id) == 0:
        available_id.append('a')

    # 16자 이상이면 거르기
    if len(available_id) >= 16:
        available_id = available_id[:15]
        # 제거 후 마침표가 끝에 위치하면 제거
        while available_id[-1] == '.':
            available_id.pop()

    # 2자 이하라면 3자가 될때까지 마지막 문자를 반복해서 끝에 붙이기
    if len(available_id) <= 2:
        # 마지막 문자
        last_char = available_id[-1]
        while len(available_id) != 3:
            available_id.append(last_char)
    #  답
    answer = ''.join(available_id)
    return answer
```



## Comment

이 문제는 원래 정규 표현식을 사용해서 푸는 문제이다... 나는 이 문제를 풀 때 정규 표현식 존재자체를 잊어버렸기 때문에 조금 엉뚱한 코드가 나와버렸다.(정답처리는 되었다.) 그렇기에 모범답안보다 두배는 긴 코드이다 ^^;; 다시 한 번 정규 표현식을 공부해야할 것 같다.



# Reference

[프로그래머스](https://programmers.co.kr)

