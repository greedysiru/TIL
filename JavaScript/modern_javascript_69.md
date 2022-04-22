# 29장. Math

* 표준 빌트인 객체
  * 생성자 함수 X
* 수학적 상수, 함수를 위한 프로퍼티 메서드 제공



## 29.1 Math 프로퍼티

### 29.1.1 Math.PI

* 원주율 PI 값



## 29.2 Math 메서드

### 29.2.1 Math.abs

* 전달된 숫자의 절대값 반환
  * 0 또는 양수



### 29.2.2 Math.round

* 인수로 전달된 소수점 이하를 반올림한 정수 반환



### 29.2.3 Math.ceil

* 인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환



### 29.2.4 Math.floor

* 인수로 전달된 소수점 이하를 내림한 정수 반환



### 29.2.5 Math.sqrt

* 전달된 숫자의 제곱근 반환



### 29.2.6 Math.random

* 임의의 난수 반환
  * 0이상 1미만



### 29.2.7 Math.pow

* 첫 번째 인수를 밑, 두 번째 인수를 지수로 거듭제곱
* ES7에서 도입된 지수 연산자를 사용하면 더 편리



### 29.2.8 Math.max

* 전달받은 인수 중에서 가장 큰 수 반환
* 배열의 요소 중에서 구하기 위해서는
  * Function.prototype.apply 메서드
  * 스프레드 문법



### 29.2.9 Math.min

* 인수 중에서 가장 작은 수 반환



## 사용 예시

```JavaScript
Math.abs(-999); // 999

Math.round(3.14) // 3

Math.ceil(3.14) // 4

Math.floor(3.14) // 3

Math.sqrt(9) // 3

Math.random(); // 랜덤한 수

Math.pow(3, 2); // 9

Math.max(10, 1, 2) // 10

Math.max.apply(null, [10, 1, 2]); // 10

Math.max(...[10, 1, 2]); // 10

MAth.min(10, 1, 2); // 1d
```

