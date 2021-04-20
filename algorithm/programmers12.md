
# [프로그래머스] 두 개 뽑아서 더하기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 두 개 뽑아서 더하기
def solution(numbers):
    # 답을 담을 배열
    answer = []
    # 주어진 숫자로 만들 수 있는 모든 숫자 배열 (중복 허용)
    numbers_sum_overlap = []
    # 주어진 숫자들로 만들 수 있는 모든 숫자 구해보기
    # 이중 for문으로 자기 자신과 같은 경우를 제외하고 다른 인덱스 더하기
    for i in range(len(numbers)):
        for j in range(len(numbers)):
            # 인덱스가 같은 경우
            if i == j:
                continue
            # 인덱스가 다른 경우 더하기
            numbers_sum_overlap.append(numbers[i] + numbers[j])
    # set 집합 자료형으로 변환후 리스트로 재 변환하여 answer에 넣기 (중복 제거)
    answer = list(set(numbers_sum_overlap))
    # 오름차순 변환
    answer.sort()
    return answer
```



## Comment

우선  이중 for문으로 주어진 숫자들로 만들 수 있는 모든 숫자를 구한 뒤, set집합 자료형으로 변환하여 중복을 제거하고 그 다음에는 다시 list로 변환하여 오름차순 변환하였다.

# Reference

[프로그래머스](https://programmers.co.kr)

