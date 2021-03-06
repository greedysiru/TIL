# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (2) (2021.3.6)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**

# 4344

[문제 링크](https://www.acmicpc.net/problem/4344)

```python
n = int(input())
for i in range(n):
    arr = list(map(int, input().split()))
    # 학생 수 뽑기
    s = arr.pop(0)
    # 평균 구하기
    avrArr = sum(arr) / len(arr)
    # 평균을 넘는 학생 수 구하기
    cnt = 0
    for j in range(len(arr)):
        if arr[j] > avrArr:
            cnt += 1
    # 비율 구하고 반올림 후 출력하기
    ratio = format((cnt / s) * 100, ".3f")
    print(ratio, "%", sep="")
```



# 4673

[문제 링크](https://www.acmicpc.net/problem/4673)

```python
# 셀프 넘버가 아닌 수를 받을 배열
check = [0] * 10001
# 셀프 넘버가 아닌 수를 배열에 체크하는 함수
def d(n):
    res = n
    # 각 자리수를 더한 후 해당 자리수를 제외하고 아래로 넘기기
    if n >= 10000:
        res += n // 10000
        n = n % 10000
    if n >= 1000:
        res += n // 1000
        n = n % 1000
    if n >= 100:
        res += n // 100
        n = n % 100
    if n >= 10:
        res += n // 10
        n = n % 10
    res += n
    # res는 셀프넘버가 아니다.
    if res <= 10000:
        check[res] = 1
    else:
        return

# 셀프넘버 탐색
for j in range(1, 10001):
    d(j)
    if check[j] == 0:
        print(j)
```



# 1157

[문제 링크](https://www.acmicpc.net/problem/1157)

## 오답

```python
string = input()
# 대문자 변환
string = string.upper()
# 단어의 길이
length = len(string)
# 단어를 체크할 딕셔너리 생성
arr = {}

# 문자열 세기
for i in range(length):
    if string[i] not in arr:
        arr[string[i]] = 1
    else:
        arr[string[i]] += 1


# 최대 반복되는 알파벳 구하기
maxWord = 0
for x in arr:
    if maxWord < arr[x]:
        maxWord = arr[x]
    # 최대 반복되는 알파벳이 둘 이상인 경우
    elif maxWord == arr[x]:
        print("?")
        break
else:
    # 최대 반복되는 알파빗이 하나인 경우
    print(max(arr, key=arr.get))
```

## 정답

```python
# 입력받고 대문자화
word = input().upper()
# set 자료형으로 중복 제거 후 인덱싱을 위해 리스트화
uniqueWord = list(set(word))
# 횟수를 셀 리스트 생성
cntArr = []
# 횟수 세기
for x in uniqueWord:
    cntArr.append(word.count(x))

# 횟수가 중복되는 경우
if cntArr.count(max(cntArr)) > 1:
    print("?")
else:
    print(uniqueWord[cntArr.index(max(cntArr))])
```

`.count()`: 찾고자하는 값이 몇개 들어있는지 확인

## Comment

딕셔너리로 푼 건 왜 안되는걸까 예외케이스 제발!!!



# 2941

[문제 링크](https://www.acmicpc.net/problem/2941)

## 오답

```python
string = input()
# 찾을 크로아티아 알파벳 리스트
alphabet = ["c=", "c-", "dz=", "d-", "lj", "nj", "s=", "z="]
# 크로아티아 알파벳 찾기
# 검사할 알파벳을 넣을 변수 문자열 선언
temp1 = ""
temp2 = ""
croa = string
end = len(string)
for i in range(0, end - 1):
    temp1 += string[i : i + 2]
    if (i + 3) <= end:
        temp2 += string[i : i + 3]
    for x in alphabet:
        if temp2 == x:
            croa = croa.replace(temp2, "C")
        if temp1 == x:
            croa = croa.replace(temp1, "C")
    temp1 = ""
    temp2 = ""
print(len(croa))
```

## 정답

```python
string = input()
# 찾을 크로아티아 알파벳 리스트
alphabet = ["c=", "c-", "dz=", "d-", "lj", "nj", "s=", "z="]
for x in alphabet:
    string = string.replace(x, "C")
print(len(string))
```

`.replace(a, b)`:  a를 b로 치환

### Comment

빙돌아가도 너무 돌아갔던 거였구나..