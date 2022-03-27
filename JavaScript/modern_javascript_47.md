# 23장 실행 컨텍스트(3)

## 23.4 실행 컨텍스트 스택

* 생성된 실행 컨텍스트는 stack 자료구조로 관리
  * 이를 실행 컨텍스트 스택이라 함
* 소스 코드 평가 -> 실행 컨텍스트 생성 -> 실행 컨텍스트 스택에 푸시
* 실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트는 언제나 실행중인 실행 컨텍스트



### 1. 전역 코드의 평가와 실행

1. 전역 코드 평가
2. 전역 실행 컨텍스트 생성
3. 실행 컨텍스트 스택에 푸시
4. 전역 변수, 전역 함수는 전역 실행 컨텍스트에 등록
5. 전역 코드 실행
6. 변수는 할당, 함수는 호출



### 2. 함수 코드의 평가와 실행

1. 코드 제어권 함수로 이동
2. 함수 코드 평가
3. 함수 실행 컨텍스트 생성
4. 실행 컨텍스트 스택에 푸시
5. 지역 변수, 지역 함수는 함수 실행 컨텍스트에 등록
6. 함수 코드 실행
7. 변수는 할당, 함수는 호출



### 3. 전역 코드로 복귀

* 모든 함수가 종료되시 제어권은 전역 코드로 이동
  - 완료된 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 팝