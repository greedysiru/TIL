# 클린코드 자바스크립트 - 배열 다루기(배열 메서드 체이닝 활용하기)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 배열 메서드 체이닝 활용하기

* 로직을 메서드 체이닝을 활용하여 명시적으로 구현할 수 있음
* for, if문의 조합으로 되어있는 로직보다는 언어 스펙에서 정의된 map, sort, filter가 표준에 가까움
  * 협업 시 동료들이 이해하기 쉬움
  * 고차함수처럼 사용
* 선언적으로 코드 작성할 수 있음
* 명확한 파이프라인으로 로직 표현
  * 자료구조의 큐와 같은 형태

```JavaScript
const price = ['2000', '1000', '3000', '5000', '4000'];

const suffixWon = (price) => price '원';
const isOverOneThousand = (price) => Number(price) > 1000;
const ascendingList = (a, b) => a - b;

const getWonPrice(priceList) => priceList
  															.filter(isOverOneThousand)
  															.sort(ascendingList)
  															.map(suffixWon);
```







## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

