# 클린코드 자바스크립트 - 경계 다루기(begin - end, first - last)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. begin, end

* 경계를 제외하는 경우
* 시작은 동일한데 끝이 다른 경우
  * 시작은 고정
* ex) 달력(date picker)
  * bigin과 end로 구분

```JavaScript
// 예약 날짜를 지정하는 함수(date picker)
const reservationDate(beginDate, endDate) => /* logic */;

// 
reservationDate('2022-12-10', '2022-12-25');
```



## 2. first, last

* 포함된 양 끝을 의미
* 부터 ~ 까지
* 양 끝점이 존재하나, 그 안의 요소들에 대한 규칙과 연속성이 보장되지 않음
* ex) DOM API
  * firstChild
  * lastChild

```JavaScript
const cats = ['siru', 'nunu', 'mango'];

const getCats = (first, last) => /* logic */

getCats('siru', 'mango');
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

