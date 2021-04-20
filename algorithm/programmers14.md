
# [프로그래머스] 소수 만들기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 소수 만들기
def solution(nums):
    answer = 0
    # 주어진 숫자 리스트의 길이
    nums_len = len(nums)

    # 합을 넣을 변수
    nums_sum = 0
    # 소수 만들기
    # 3중 for문으로 조합을 만들어 합구하기
    for i in range(nums_len):
        for j in range(i + 1, nums_len):
            for k in range(j + 1, nums_len):
                # 조합의 합
                nums_sum = nums[i] + nums[j] + nums[k]
                # 구해진 합을 기준으로 2부터 자기자신 -1 까지 나누었을 때 0이 되면 소수가 아니다.
                for l in range(2, nums_sum):
                    if nums_sum % l == 0:
                        break
                # break에 걸리지 않았으면 소수
                else:
                    answer += 1
    return answer
```



## Comment

소수의 정의를 깜빡하는 바람에 올바른 코드를 처음에 작성했음에도 불구하고 엄청나게 돌아간 문제... 삼중 for문으로 조합을 구해냈으나 if문으로 소수를 필터링하는 과정에서 엉뚱하게도 숫자 % 2 == 1인 경우를 소수로 판별하였기 때문에 올바른 답이 나오지 않았었다.... 문제의 지문를 잘 읽고 해당하는 개념을 내가 잘 이해하고 있는지 점검하며 문제를 접근해야겠다.

# Reference

[프로그래머스](https://programmers.co.kr)

