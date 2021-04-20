
# [프로그래머스] 음양 더하기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 음양 더하기
def solution(absolutes, signs):
    # signs가 참이면 해당 absolutes의 수가 양수, 거짓이면 음수
    # 주어진 수를 하나씩 접근
    # 양수, 음수가 적용된 실제 합
    answer = 0
    for i in range(len(absolutes)):
        #  참인경우 양수이므로 더하기
        if signs[i]:
            answer += absolutes[i]
        # 거짓인 경우 음수이므로 빼기
        else:
            answer -= absolutes[i]
    return answer
```



## Comment

absolutes와 signs의 길이는 같으므로 단일 for문으로 동일한 인덱스에서 signs이 ture이면 양수처리, false이면 음수처리를 하여 답을 도출하면 된다.

# Reference

[프로그래머스](https://programmers.co.kr)

