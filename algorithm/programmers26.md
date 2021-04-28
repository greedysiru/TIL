




# [프로그래머스] 다음 큰 숫자 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 다음 큰 숫자
def solution(n):
    answer = 0
    # n을 2진수로 변환 후 문자열로 바꾸기
    n_bin = str(bin(n))
    # 1의 갯수
    one_count = n_bin.count('1')
    # 조건을 충족하는 수가 나올 때 까지 반복
    while True:
        n += 1
        # 2진수로 변환 후 문자열로 바꾸기
        next_bin = str(bin(n))
        # 1의 갯수가 n의 1의 갯수와 같으면 정답처리 후 중단
        if one_count == next_bin.count('1'):
            answer = int(n)
            break
    return answer
```



## Comment

내 코드가 평가가 좋은 답안과 거의 비슷했다!

파이썬에서 정수를 이진수를 변환하는 내장함수인 bin이 있어서 편하게 변환할 수 있었다.그 이후, 문자열로 바꾸어서 1의 갯수를 세어 주어진 두 조건을 충족(n보다 클것, 1의 갯수가 같을 것)하면 된다.

# Reference

[프로그래머스](https://programmers.co.kr)