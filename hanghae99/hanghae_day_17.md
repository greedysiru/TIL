# [항해99 1기] [Chapter2-2] 자료구조, 알고리즘 (15) (2021.3.17)

**알고리즘 문제를 풀면서 알게된 팁들**



## 01. 시간초과가 발생할 때

* 코드 자체의 시간 복잡도
  * 반복문을 너무 많이 사용한 것이 아닌지 체크
  * 적절하지 않은 자료구조를 사용한 것이 아닌지 체크
  * 예를 들어, pop(0)보다 popleft()가 더 빠르다.
* 빠르게 입력 받기를 시도해본다

```python
# sys 라이브러리
import sys

data = sys.stdin.readline().rstrip()
```



## 02. 오류가 발생할 때

* 디버깅 모드로 분석한다.
  * 코드를 작성했을 때 나의 의도와 다른 변수의 변화 등을 체크
* 인덱스 오류
  * 보통 for문에서 발생한다.
  * 입력이 아주 짧은 경우 발생할 수도 있다.
  * 메모이제이션으로 리스트의 일정 인덱스의 값을 선언해놓았을 때 발생 가능
* 자료형 오류
  * 입력을 받았을 때 map 함수 처리를 안 했을 가능성이 있다.
  * 코드에서 자료형이 적절하게 되어있는지 점검



## 03. 예외 케이스

* 예제 케이스는 통과했지만 채점에서 오답처리가 되는 경우
* 코드 상에서 고려하지 못한 것을 점검
* 경험상, 0이나 1같은 작은 값에서 많이 발생하게 되므로 직접 넣어볼 것
* -1(음수), 문제에서 주어진 최댓값, 최솟값을 고려하기
* 또는, 만든 입력값을 넣어봤을 때 예상하는 답과 다른지 체크
  * 다른 경우, 디버깅 모드로 예상하는 값과 왜 다른지 점검
* [파이썬 튜터](http://pythontutor.com/)에서 시각화된 코드의 진행을 보는 것도 좋다.





