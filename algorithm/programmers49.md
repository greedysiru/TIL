# [프로그래머스] 튜플 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 튜플
def solution(s):
    answer = []
    # 입력받은 s 문자열의 괄호와 끝 괄호를 제거하고 리스트 형태로 변환
    s_list = s.replace('{', '').replace('}}', '').split('},')
    # 각 원소의 길이를 기준으로 정렬
    s_list.sort(key=len)
    # s_list의 문자열을 각각 접근
    for string in s_list:
        # 문자열을 정수화 하고 리스트화 하여 nubmers에 넣기
        numbers = list(map(int, string.split(',')))
        # numbers의 숫자를 하나씩 접근하며 답 리스트에 없는 경우에만 append
        for number in numbers:
            if number not in answer:
                answer.append(number)
    return answer
```



## Comment

입력받은 s를 리스트로 변환한다. 그 이후에는 만들어진 리스트의 요소를 하나씩 접근하며 answer 리스트에 중복이 되지 않도록 `not in`을 사용하여 하나씩 `append`한다. 여기서, 핵심은 

- {{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}
- {{2, 1, 3, 4}, {2}, {2, 1, 3}, {2, 1}}
- {{1, 2, 3}, {2, 1}, {1, 2, 4, 3}, {2}}

일때 다 같은 튜플인 (2, 1, 3, 4)이다.

그러므로 세 번째의 경우에는 리스트로 변환하면, [[1, 2, 3], [2, 1], [1, 2, 4, 3], [2]]인데, 이 리스트를 하나씩 접근하여 튜플을 만들기 위해서는 우선 만들어진 리스트를 길이를 기준으로 sort를 하기 위해서` s_list.sort( key = len)`을 실행해준다. 만약, 길이를 기준으로 정렬을 하지 않는다면, [1, 2, 3, 4]가 만들어질 것이다. loop문으로 앞에서부터 접근하기 때문이다.

# Reference

[프로그래머스](https://programmers.co.kr)

