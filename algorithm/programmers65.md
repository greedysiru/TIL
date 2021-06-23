# [프로그래머스] 문자열 압축 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 문자열 압축
def solution(s):
    answer = []
    for i in range(1, len(s) + 1):
        # 압축된 문자열을 나타내는 리스트
        compressed_list = []
        # 시작 인덱스
        start = 0
        # 끝 인덱스
        end = i
        # 주어진 문자열 s를 나누기
        # 끝 인덱스가 주어진 s의 길이 이하일때 실행
        while end <= len(s):
            # 문자열  s를 start부터 end - 1까지 가져오기
            slice_string = s[start: end]
            compressed_list.append(slice_string)
            # 다음 루프를 위해, start에는 end를 입력하고 end는 i만큼 더하기
            start = end
            end += i
        # start가 문자열 s길이 이하일 때 나머지 문자열 슬라이싱하여 append
        if start < len(s):
            compressed_list.append(s[start:len(s) + 1])
        # 압축된 문자열의 길이 재기
        count = 1
        # 압축된 문자열을 넣을 변수
        compressed_string = ''
        # 만들어진 압축된 문자열 리스트를 1번 인덱스부터 끝가지 하나씩 접근
        for j in range(1, len(compressed_list)):
            # 이전 문자열과 현재 문자열이 같은 경우
            if compressed_list[j - 1] == compressed_list[j]:
                # 압축이 되는 것이므로 +1
                count += 1
            # 다른경우
            else:
                # 카운트가 1을 초과
                if count > 1:
                    # 그만큼 압축이 된 것이므로 count를 문자열화하여 넣고 압축된 문자열도 이어서 넣기
                    compressed_string += str(count) + compressed_list[j - 1]
                # 1인경우
                else:
                    # 압축이 되지 않은 것이므로 count는 생략하고 문자열 넣기
                    compressed_string += compressed_list[j - 1]
                count = 1
        # 루프문이 끝나고 나머지 문자열 처리하기
        if count > 1:
            # 카운트가 1이 넘으면 압축된 것이므로 count를 넣고 압축된 문자열 넣기
            compressed_string += str(count) + compressed_list[j - 1]
        else:
            # 압축된 문자열 리스트가 1인경우
            if len(compressed_list) == 1:
                # 0번인덱스에 s가 그대로 들어있으므로 넣는다.
                compressed_string += compressed_list[0]
            else:
                # 나머지 문자열 넣기
                compressed_string += compressed_list[j]
        # answer에 만들어진 압축된 문자열 길이를 append
        answer.append(len(compressed_string))
    # 가장 최솟값을 return
    return min(answer)
```



## Comment

완전탐색 문제. 주어진 문자열을 나눈다. 나눌 때, 나누는 단위를 1에서부터 문자열 전체길이까지 `for`문으로 나누도록 하고 이때 나누어진 각 문자열은 별도에 리스트에 `append`한다. 

나누어진 문자열이 담긴 리스트를 다시` for`문으로 각 요소를 접근하며 실제 압축된 문자열을 만든다. 이전요소와 현재요소가 같은지, 다른지를 `if`문으로 분류하여 처리한다., 같은 경우에는 압축이 가능한 것이므로 `count`를 `+1`하고 다른 경우는 이전까지의 압축된 문자열을 표시해야 하므로 `count`가 1일때는 문자열만 넣고 1을 초과할 때는 압축된 수와 문자열을 함께 넣는다. 그리고 `count`를 다시 1로  초기화한다. 이때, 넣는 문자열은 이전 요소의 문자열임을 유의해야한다. 

만들어진 압축된 문자열의 길이를 `answer`에 `append`하여 최종적으로  `answer`를 `min`함수로 처리해서 최솟값이 `return`되도록 한다.

# Reference

[프로그래머스](https://programmers.co.kr)