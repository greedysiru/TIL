# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (15)(2021.2.8)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**

# 1. 응급실(큐)

## 나의 전략

* 1 순위: 위험도, 2 순위: 순서
  - 순서대로 환자를 검사하고 위험도가 그 환자보다 높은지 본다.
* **deque 자료구조**
  * **popleft**로 뽑아내서 검사
* **튜플**

## 문제 풀이

```python
from collections import deque
n, m = map(int, input().split()); # n: 환자 수 , m번째 환자
a = list(map(int, input().split())); # 위험도
dan = []; # 환자받을 리스트
for x in enumerate(a): # 튜플로 입력
    dan.append(x);
dan = deque(dan); # deque
target = dan[m]; # 목표 환자
cnt = 0; # 카운트
p = 0; # 환자 위험도
while dan:
    p = dan.popleft();
    for x in dan:
        if p[1] < x[1]:
            dan.append(p);
            p = 0;
            break;
    if p == target: # 목표환자를 찾은 경우
        cnt += 1;
        print(cnt);
        break;
    elif p != 0:
        cnt += 1;
```



## 문제 해설

* 같은 위험도가 있을 때를 고려
* deque 자료구조
* **튜플**
  * 리스트 생성식(표현식) 사용할것
* **any함수**
  * **조건에서 단 한 번이라도 참이라면, 명령 참 출력**



## 문제 답안

```python
from collections import deque
n, m = map(int, input().split());
# 리스트에 입력을 받아 인덱스(pos)와 val로 튜플 생성
Q = [(pos, val) for pos, val in enumerate(list(map(int, input().split())))];
Q = deque(Q); # deque
cnt = 0; # 카운트

while True:
    cur = Q.popleft();
    if any(cur[1] < x[1] for x in Q): # Q의 원소 하나하나 접근하여 비교
        Q.append(cur); # 위험도가 높은 사람 한 사람이라도 있는 경우
    else: # 진료 받는 경우
        cnt += 1;
        if cur[0] == m: # 목표로 하는 환자
            print(cnt);
            break
```



## 풀이와 답안 비교

리스트 생성식과 any함수 익숙해지기!!



# 2. 교육과정 설계(큐)

## 나의 전략

* 전체 수업계획을 리스트 -> **deque**

* 원소를 하나하나 탐색하면서 **popleft**

* 필수과목에 포함된 원소는 별도의 리스트에 담기

  * 맞는 순서인지 검사

  

## 문제 풀이

```python
from collections import deque
p = input(); # 필수과목
p = list(p); # 리스트화
n = int(input());
cnt = 0; # 카운트
for _ in range(n):
    a = []; # 확인 리스트
    le = input();
    le = deque(le);
    while le: # 수업설계 확인
        b = le.popleft();
        if b in p: # 필수 과목인 경우
            a.append(b);
    cnt += 1;
    if a == p:
        print("#%d YES" %cnt);
    else:
        print("#%d NO" %cnt);
```



## 문제 해설

* 필수 과목은 리스트화

* 수업계획은 deque

  * 원소 하나하나가 필수 과목인지 확인

  * 원소가 필수과목이면 **필수 과목의 리스트 pop**

    * pop을 했을 때, 수업계획의 원소와 return이 다르다면 순서가 다른것이다.

  * **필수과목 리스트가 비어있으면 YES**

    

## 문제 답안

```python
from collections import deque
need = input();
n = int(input());
for i in range(n):
    plan = input();
    dq = deque(need); # deque화
    for x in plan: # 과목 탐색
        if x in dq: # 필수과목일 경우
            if x != dq.popleft(): # 필수과목의 맨 앞자료와 일치하지 않을 때
                print("#%d NO" %(i + 1));
                break;
    else: # 순서가 맞는 경우
        if len(dq) == 0: # 모든 필수과목이 확인된 경우
            print("#%d YES" %(i + 1));
        else:
            print("#%d NO" %(i + 1));
```



## 풀이와 답안 비교

잘 푼 것 같다.

여기서, for-else 문은 for문이  조건문에 의해 break가 안 되었을 경우의 수행 코드를 작성할 수 있다.



# 3. 단어찾기(해쉬)

## 문제 해설

* 딕셔너리 자료형 사용하기
  * 값을 1로 초기화
  * 단어가 다시 사용되면 0으로 바꾸기
  * 1인 key값을 출력

## 문제 답안

```python
n = int(input());
p = dict(); # 빈 딕셔너리
for i in range(n): # 단어 입력 받기
    word = input();
    p[word] = 1; # 딕셔너리 입력
for i in range(n - 1): # 시의 단어 탐색
    word = input();
    p[word] = 0;

for key, val in p.items(): # 딕셔너리 키와 값 접근
    if val == 1:
        print(key);
        break;
```



## 풀이와 답안 비교

딕셔너리를 까먹어서 강의를 봤는데, 생각보다 너무 쉬웠다..



# 4. Anagram(아나그램 : 구글 인터뷰 문제)

## 나의 전략

* 딕셔너리 자료형 사용

  

## 문제 풀이

```python
a = input();
b = input();
dictA = dict();
dictB = dict();
for x in a:
    dictA[x] = dictA.get(x, 0) + 1;
for x in b:
    dictB[x] = dictB.get(x, 0) + 1;

for y in dictA.keys(): # 아나그램 검사
    if dictA[y] != dictB[y]:
        print("NO");
        break;
else:
    print("YES");
```



## 문제 해설

* **두 딕셔너리를 만들어서 알파벳을 카운팅**
  * 키값을 비교해서 아나그램인지 판별
* 딕셔너리 내장함수 **.get** 사용
  * **dic.get('A', 0)** : 딕셔너리에 'A'가 있으면 그 값을 return, 없으면 0을 return
* **아스키 코드(알파벳)**
  * 대문자 : 65 ~ 90
  * 소문자 : 97 ~ 122

## 문제 답안

```python
a = input();
b = input();
str1 = dict(); # 비교를 위한 딕셔너리
str2 = dict();

for x in a: # 알파벳 카운팅
    str1[x] = str1.get(x, 0) + 1;
for x in b:
    str2[x] = str2.get(x, 0) + 1;

for i in str1.keys(): # str1 키 접근
    if i in str2.keys(): # str1과 str2의 key값이 똑같이 있는지
        if str1[i] != str2[i]: # 값이 같은지
            print("NO");
            break;
    else:              # str1과 str2의 key값이 다른 경우
        print("NO");
        break;
else: # 아나그램이면
    print("YES");
```



## 개선된 코드

```python
a = input();
b = input();
sH = dict();

for x in a: # 알파벳 카운팅
    sH[x] = sH.get(x, 0) + 1;
for x in b:
    sH[x] = sH.get(x, 0) - 1; # 두 문자열이 같다면 value가 0이 될 것

for x in a:
    if sH.get(x) > 0:
        print("NO")
        break;
else:
    print("YES");
```



## 리스트 해쉬

```python
a = input();
b = input();
str1 = [0]*52; # 알파벳 대문자,소문자의 총 개수
str2 = [0]*52;

for x in a:
    if x.isupper(): # 대문자인 경우
        str1[ord(x) - 65] += 1; # 아스키코드로 변환 후 해싱(인덱스 0부터)
    else:
        str1[ord(x) - 71] += 1; # 소문자는 26번부터 해싱

for x in b:
    if x.isupper(): # 대문자인 경우
        str2[ord(x) - 65] += 1; # 아스키코드로 변환 후 해싱(인덱스 0부터)
    else:
        str2[ord(x) - 71] += 1; # 소문자는 26번부터 해싱

for i in range(52):
    if str1[i] != str2[i]:
        print("NO");
        break;
else: 
    print("YES");
```

* 알파벳 대문자, 소문자를 받을 빈 리스트 생성
* 각 빈 리스트의 **0~25번 인덱스에는 대문자**를 해싱
* 각 빈 리스트의 **26 ~ 51번 인덱스에는 소문자**를 해싱
* 아스키 코드값을 인덱스로 사용하도록 각 경우에서 적절한 값을 빼준다.



## 풀이와 답안 비교

강의를 조금 참조했지만, 잘 풀었다.

면접을 대비해서 리스트 해쉬 풀이도 기억해 두자.