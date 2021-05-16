


# [프로그래머스] 순위 검색 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 해결 방법

* 시간복잡도가 중요한 문제
* query가 매개변수로 주어질 때, 해당하는 사람들의 숫자를 배열에 담아 반환
  * query 배열의 크기는 최대 100,000
  * info 배열의 크기는 최대 50,000
  * query * info를 따져봤을 때 시간복잡도에서 오답처리가 된다는 것을 예측할 수 있다.
* 효율적인 방식
  * **Hash Table** : 특정 값을 검색할 때 O(1)
  * query의 경우의 수를 다 구해서 hash key로 만들기
  * hash key를 충족하는 지원자의 점수를 key 값에 배열로 넣기
  * 각 hash key에 들어가 있는 점수 배열을 정렬
  * 이분 탐색으로 원하는 결과를 찾기



## 파이썬 코드

```python
# 순위 검색
from itertools import combinations


# combinations를 이용해서 모든 조합을 만들기
# 유저의 info에 따라 나올 수 있는 모든 query의 경우의 수
def make_all_cases(user_info_array):
    all_cases_from_user = []
    # 유저 정보에 0개의 조건 ~ 4개의 조건이 있을 때를 구하기
    for i in range(5):
        # 만들어진 조합을 하나씩 빼기
        for combination in combinations([0, 1, 2, 3], i):
            case = ''
            # 0 ~ 3 까지 해당 수가 조합에 들어있는지 보기
            for j in range(4):
                # 들어있으면 해당 정보를 넣기
                if j in combination:
                    case += user_info_array[j]
                # 들어있지 않으면 -를 넣기
                else:
                    case += "-"
            all_cases_from_user.append(case)
    return all_cases_from_user

# 이분 탐색
# 쿼리의 점수를 점수 배열(해시테이블)에서 찾기
# 최솟값을 넘는 최소 인덱스 시점을 찾을 수 있다.
def get_lower_bound(target, array):
    # 최솟값
    current_min = 0
    # 최댓값
    current_max = len(array)

    while current_min < current_max:
        # 시돗값
        current_guess = (current_min + current_max) // 2
        # 시돗값이 target보다 큰 경우 최댓값에 시돗값 대입
        if array[current_guess] >= target:
            current_max = current_guess
        # 작은 경우 최솟값에 시돗값 + 1을 대입
        else:
            current_min = current_guess + 1
    
    return current_max

def solution(info, query):
    # 답
    answer = []
    # 쿼리 결과를 담을 Hash Table
    all_cases_from_users = {}
    # info를 공백을 기준으로 배열로 바꾸기
    for user_info in info:
        user_info_array = user_info.split()
        # 유저 정보 배열을 함수에 넣기
        all_cases_from_user = make_all_cases(user_info_array)
        # 유저 정보 배열을 통해서 만들어진 쿼리 조건을 하나씩 빼기
        for case in all_cases_from_user:
            # 각 조건이 hash table의 key에 없으면 생성 후 점수를 넣기
            if case not in all_cases_from_users.keys():
                all_cases_from_users[case] = [int(user_info_array[4])]
            # 이미 key로 존재하는 경우 해당 key에 점수를 넣기
            else:
                all_cases_from_users[case].append(int(user_info_array[4]))

    # 정렬하기
    # key를 하나씩 빼내서 각 key의 점수를 정렬
    for key in all_cases_from_users.keys():
        all_cases_from_users[key].sort()
                
    # 문제에서 입력받은 쿼리를 배열로 바꾸기 (공백 기준)
    for query_info in query:
        query_info_array = query_info.split()
        # and를 제외하고 유효한 값을 선택해서 case로 만들기
        case = query_info_array[0] + query_info_array[2] + query_info_array[4] + query_info_array[6]
        # case가 hash table에 존재하는 경우
        if case in all_cases_from_users.keys():
            # hash table의 점수를 가져오기 (배열)
            target_users = all_cases_from_users[case]
            # 쿼리의 점수와 hash table의 점수 배열을 넣기
            # 점수 배열의 길이에 함수로인해 return된 최소 인덱스 시점을 뺀다 (충족하는 사람 수)
            answer.append(
                len(target_users) - get_lower_bound(int(query_info_array[7]), target_users)
            )
        else:
            answer.append(0)

    return answer
```



## Comment

2021 카카오 블라인드 채용의 문제.

혼자서 3시간동안 헤매다가 결국 답안을 참고하고 분석하여 풀어냈다.

어떤 원리인지는 이해가 되긴 하나, 안 보고 저 코드를 구현하기까지 공부가 더 필요하다.

# Reference

[프로그래머스](https://programmers.co.kr)