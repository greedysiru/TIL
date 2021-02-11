# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (19)(2021.2.11)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 전역변수와 지역변수

## 정수 자료형인 경우

```python
def DFS1():
    print(cnt);  # 5 출력
    
def DFS2():
    cnt = 3; # 지역변수 생성
    print(cnt); # 3 출력
    
def DFS3():
    if cnt == 5: # error
        cnt = cnt + 1; # 지역변수 생성, cnt에 1을 더해야하는데, 이 시점에서는 cnt가 없음
        print(cnt);

def DFS4():
    global cnt; # cnt는 전역변수라고 선언
    if cnt == 5: 
        cnt = cnt + 1;
        print(cnt); # 6 출력
        
if __name__=="__main__": 
    cnt = 5; # 전역변수
    DFS1();
    DFS2();
    DFS3();
    DFS4();
    print(cnt); # 6 출력
```

* 전역변수 : 메인스크립트에서 선언된 변수
  * **모든 함수가 접근하거나 값을 변경할 수 있다.**
* DFS1(), DFS2(), DFS3(), DFS4() 에서
  * **cnt**가 자신의 **지역변수인지 확인**한다.
  * 없다면, **전역변수인지 확인**한다.
  * 아예 선언되지 않은 변수라면, 오류 발생
  * **지역변수가 전역변수에 우선한다.**
* 함수 내에서 전역변수로 선언된 경우(**global**)
  * 함수내에서 변수의 변화가 전역에서도 적용된다.



## 리스트 자료형인 경우

```python
def DFS1():
    a[0] = 7; # 값을 변경
    print(a); # [7, 2, 3] 출력
    
def DFS2():
    a = [7, 8]; # 리스트 생성
    print(a); # [7, 8] 출력
    
def DFS3(): #  error
    a = a + [4]; # 리스트 생성, 이 시점에서 a리스트는 없다.
    print(a);
    
if __name__ == "__main__":
    a = [1, 2, 3];
    DFS1();
    DFS2();
    DFS3();
    print(a) # [7, 2, 3] 출력
```

* 함수내에서 **리스트 인덱스를 참조하는 경우**
  * **로컬 리스트가 아닌 전역 리스트로 인식한다.**
* 함수내에서 리스트를 새로 선언하는 경우
  * 로컬 리스트로 생성된다.
* 함수 내에서 리스트를 전역 리스트로 사용하고 싶다면 **global 사용**



# 1. 부분집합 구하기(DFS)

## 문제 해설

* DFS
* **상태트리** : 하나의 함수가 호출되면 두 상태트리로 나뉘어 각각 함수를 호출
  * 함수를 사용하는 상태 트리
  * 함수를 사용하지 않는 상태 트리
* 각 **원소들의 출력여부를 체크**하는 변수를 리스트로 생성
* 자연수 n을 입력받았을 때, **재귀함수는 n +1 시점에서 출력 체크된 부분집합을 출력한다.**

## 문제 답안

```python
def DFS(v):
    if v == n + 1: # n + 1이면 출력
        for i in range(1, n + 1):
            if ch[i] == 1:
                print(i, end = " ");
        print();
    else: # 부분집합 만들기
        ch[v] = 1 # 해당 원소를 사용한다
        DFS(v + 1);
        ch[v] = 0; # 해당 원소를 사용하지 않는다
        DFS(v + 1);
if __name__ == "__main__" :
    n = int(input());
    ch = [0]*(n + 1); # 체크 변수
    DFS(1);
```



# 2. 합이 같은 부분집합(DFS : 아마존 인터뷰)

## 문제 해설

* 주어진 집합에서 두 부분집합을 만든다.
* **전체원소의 합(total) - 부분집합의 합(sum) = 또 다른 부분집합의 합**
* **상태트리 계획할 것**
  * **인덱스(트리에서는 레벨)**와 각 **부분집합의 합을 누적하는 함수**를 사용하기
  * **인덱스**의 원소를 사용하는 경우와 사용하지 않는 경우
* **시간복잡도 줄이기**
  * 부분집합의 합이 총합의 절반을 넘으면, 그 부분집합에서 재귀함수를 호출 중단
  * 절반을 넘은 것이면 다른 부분집합과 같아질 수 없기 때문이다.



## 문제 풀이

```python
def DFS(v):
    if v == n + 1: # n + 1이면 출력
        subS = []; # 부분집합 초기화
        for i in range(1, n + 1):
            if ch[i] == 1:
                subS.append(s[i - 1]);
        subSetSum = sum(subS);
        if  subSetSum == totalSum - subSetSum:
            print("YES");
            sys.exit(0); # 종료
 
    else: # 부분집합 만들기
        ch[v] = 1 # 해당 원소를 사용한다
        DFS(v + 1);
        ch[v] = 0; # 해당 원소를 사용하지 않는다
        DFS(v + 1);

if __name__ == "__main__" :
    n = int(input());
    s = list(map(int, input().split()));
    ch = [0]*(n + 1); # 체크 변수
    totalSum = sum(s); # 전체 집합의 합계
    DFS(1);
    print("NO");
```



## 문제 답안

```python
def DFS(L, sum):
    if sum > total//2 : # 시간 복잡도 줄이기
        return;
    if L == n: # n이 종료지점
        if sum == (total - sum):
            print("YES");
            sys.exit(0); # 프로그램 종료
    else:
        DFS(L + 1, sum + a[L]); # 부분집합을 사용하여 합 누적
        DFS(L + 1, sum); # 합을 누적하지 않음

if __name__ == "__main__" :
    n = int(input());
    a = list(map(int, input().split()));
    total = sum(a); # a의 총합
    DFS(0, 0);
    print("NO"); # 프로그램이 종료되지 않고 함수가 끝난 경우
```



## 풀이와 답안 비교

답은 잘 나왔지만, 내 코드는 시간복잡도가 높을 것이다. DFS는 개념은 이해되지만, 적용하기 어려운 것 같다. 숙달될 때까지 상태트리를 직접 그려보고 코드를 작성해야할 것 같다.