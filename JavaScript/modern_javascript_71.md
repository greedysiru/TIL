# 30장. Date(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**

## 30.2 Date 메서드

### 30.2.1 Date.now

* 1970년 1월 1일 00:00:00(UTC) 기점으로 현재 시간까지 경과한 밀리초 숫자로 반환



### 30.2.2 Date.parse

* 1970년 1월 1일 00:00:00(UTC) 기점으로 인수로 전달된 지정 시간 까지의 밀리초를 숫자로 반환



### 30.2.3 Date.UTC

* 1970년 1월 1일 00:00:00(UTC) 기점으로 인수로 전달된 지정 시간까지 밀리초를 숫자로 반환
* new Date(yaer, month, [, day, hour, minute, second, millisecond])와 같은 형식의 인수를 사용해야 함



### 30.2.4 Date.prototype.getFullYear

* Date 객체의 연도를 나타내는 정수 반환



### 30.2.5 Date.prototype.setFullYear

* Date 객체에 연도를 나타내는 정수 설정



### 30.2.6 Date.prototype.getMonth

* Date 객체의 원을 나타내는 0 ~ 11 정수를 반환
  * Date 객체에서의 월은 0부터 시작



### 30.2.7 Date.prototype.setMonth

* Date 객체의 월을 설정
* 옵션으로 일을 설정 가능



### 30.2.8 Date.prototype.getDate

* Date 객체의 날짜 정수 반환



### 30.2.9 Date.prototype.setDate

* Date 객체 날짜 정수 설정



### 30.2.10Date.prototype.getDay

* Date 객체의 요일을 나타내는 0 ~ 6 반환



### 30.2.11 Date.prototype.getHours

* Date 객체 시간을 나나태는 정수 반환



### 30.2.12 Date.prototype.setHours

* Date 객체에 시간(0 ~ 23)을 나타내는 정수 설정
  * 분, 초, 밀리초 설정 가능



### 30.2.13 Date.prototype.getMinutes

* Date 객체의 분(0 ~ 59)을 나타내는 정수 반환



### 30.2.14 Date.prototype.setMinutes

* Date 객체에 분(0 ~ 59)을 나타내는 정수 설정
  * 초, 밀리초 설정 가능



### 30.2.15 Date.prototype.getSeconds

* Date 객체의 초(0 ~ 59)를 나타내는 정수 반환



### 30.2.16 Date.prototype.setSeconds

* Date 객체에 초(0 ~ 59)를 나타내는 정수를 설정
  * 밀리초 설정 가능



### 30.2.17 Date.prototype.getMilliseconds

* Date 객체의 밀리초를 나타내는 정수 반환



### 30.2.18 Date.prototype.setMilliseconds

* Date 객체에 밀리초(0 ~ 999)를 나타내는 정수 설정



### 30.2.19 Date.prototype.getTime

* 1970년 1월 1일 00:00:00(UTC) 기점으로 Date 객체의 시간까지 경과된 밀리초 반환



### 30.2.20 Date.prototype.setTime

* 1970년 1월 1일 00:00:00(UTC)를 기점으로 경과된 밀리초 설정



### 30.2.21 Dat.prototype.getTimezonOffset

* UTC와 Date 객체에 지정된 로캘 시간과의 차이를 분 단위로 반환



### 30.2.22 Date.prototype.toDateString

* 사람이 읽을 수 있는 형식으로 Date 객체의 날짜 반환



### 30.2.23 Date.prototype.toTimeString

* 사람이 읽을 수 있는 형식으로 Date 객체의 시간을 표현한 문자열 반환



### 30.2.24 Date.prototype.toISOString

* ISO 8601 형식으로 Date 객체의 날짜와 시간을 표현한 문자열 반환



### 30.2.25 Date.prototype.toLocaleString

* 전달한 로캘을 기준으로 Date 객체의 날짜, 시간을 표현한 문자열 반환
  * 생략시, 시스템의 로캘을 적용



### 30.2.26 Date.prototype.toLocaleTimeString

* 인수로 전달한 로캘 기준으로 Date 객체의 시간을 표현한 문자열 반환
  * 생략시, 시스템 로캘 적용

