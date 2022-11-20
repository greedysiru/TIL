# 기초 JS, CS 상식 - 유니코드



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 1. 문자를 다루는 방식들

### CCS(Coded Character Set)

* 문자들을 Code Point에 대응시켜 만든 코드화된 문자들의 집합
  * Code Point: 정의해둔 정수값, 각 문자들의 식별자가 됨
* Code Point는 Character의 식별자가 됨
* ex) KS C 5601, ISO 10646, US-ASCII ...



### CES(Character Encoding Scheme)

* CSS를 octet(8bit) 집합에 대응
* CSS와 CES는 1:1로 대응
* 인코딩에 해당함
  * 인코딩: Characther를 시스템이 인식할 수 있는 값으로 변환
  * 디코딩: 인코딩된 값을 다시 Character로 변환
* UTF-8, UTF-16, euc-kr, CP949



### TES(Transfer Encoding Syntax)

* 인코딩한 문자가 특정 프로토콜을 타고 전송되도록 변환하는 것
* 통신 프로토콜에 제약이 있을 수 있기 때문
  * ex) URL에서는 공백 사용 불가
* URL Encoding, BASE64 Encoding



## 2. 유니코드란

* 다양한 문자가 표현될 수 있는 이유
* 다양한 나라가 서로 다른 인코딩 방식을 사용함으로, 호환성 및 확장성에 문제가 일어남
  * 이를 방지하기 위해, 전 세계 문자를 컴퓨터에서 다룰 수 있도록 표준 시스템을 정의
* 대부분의 문자와 이모티콘 포함
* 브라우저에서는 값인 문자가 글꼴을 만나 렌더링이 됨
* 현재도 꾸준히 추가되는 중
* 4바이트를 사용
* BMP 영역
  * 현재 쓰이는 대부분의 문자 정의



### 유니코드 - CCS

* 코드 포인트 범위 - 0x0 ~ 0x10FFFF
  * 1114112개 문자
* Surrogate Pair 방법을 이용해 2바이트보다 큰 문자를 표현
  * Surrogate 영역에 있는 보조 문자와 BMP 외부 영역의 문자를 합쳐 한 글자 표현



### 유니코드 - CES

* Code Point가 어떤 단위로 조합되어 인코딩되는 지 정의
* UTF 계열
  * 숫자는 어떤 단위로 조합하여 인코딩되어 있는지 표현
  * 웹은 크기를 줄이기 위해 UTF-8을 주로 사용
* Big-Endian, Little-Endian
  * 컴퓨터 메모리에 저장된 바이트의 순서
  * Big-Endian은 큰 쪽에서 작은 쪽으로 저장
  * Little-Endian은 작은 쪽에서 큰 쪽으로 저장
* BOM(Byte Order Mark)
  * 문서 제일 앞에 U+FEFF를 삽입하여, 어플리케이션이 바이트 순서를 알 수 있게 해 줌
  * UTF-8은 엔디안이 의미가 없어 BOM이 없어도 상관 없음



## 3. JavaScript에서의 unicode

* 브라우저를 따라 unicode 지원
* 이모지는 4바이트
  * 각 코드 포인트가 2개
  * Surrogate Pair
  * 문자 길이를 2 차지
* \u를 통해 유니코드 문자 표현 가능
* 유니코드에서 영어, 한글 상관없이 2바이트로 읽힘
  * 한글은 한 글자당 1 차지



## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

