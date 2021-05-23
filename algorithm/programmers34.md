
# [프로그래머스] 영어 끝말잇기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
from collections import deque
# 영어 끝말잇기
def solution(n, words):
    answer = []
    # 리스트를 deque 자료형으로 변환
    words_q = deque(words)
    # 사용된 단어를 넣을 리스트
    # 가장 첫번째 단어를 넣어 초기화
    used_words = []
    used_words.append(words_q.popleft())
    # 카운트
    cnt = 1
    # words_q 의 단어를 하나씩 빼기
    while words_q:
        # 사용된 단어
        word = words_q.popleft()
        # 해당 단어가 used_words에 없는 경우
        if word not in used_words:
            # 끝말잇기 규칙을 지킨 경우
            if used_words[-1][-1] == word[0]:
                used_words.append(word)
            # 지키지 않은 경우
            else:
                answer = [(len(used_words) % n) + 1,
                          (len(used_words) // n) + 1]
                break
        # 해당 단어가 used_words에 있는 경우
        elif word in used_words:
            answer = [(len(used_words) % n) + 1, (len(used_words) // n) + 1]
            break
        cnt += 1
    # 탈락자가 없는 경우
    else:
        answer = [0, 0]
    print(used_words)
    return answer
```



## Comment

주어진 단어 리스트를  deque로 변환하여 하나씩 빼며 끝말잇기의 조건을 충족할 때만 while이 실행되도록 하였다.

answer에 담을 숫자는 사용된 단어 리스트의 길이의 몫, 나머지 관계를 응용하여 해당 인덱스에 넣었다.

# Reference

[프로그래머스](https://programmers.co.kr)