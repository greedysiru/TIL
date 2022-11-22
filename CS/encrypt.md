# 기초 JS, CS 상식 - 암호화 기초



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 암호화

* 평문(Plaintext)을 해독할 수 없는 암호문(Ciphertext)로 반환
* 단방향(해싱)과 양방향 암호화 존재



### 1. 단방향 암호화

* 해시 알고리즘을 이용하여, 평문을 복호화할 수 없는 형태로 암호화
  * 저장하는 측에서 해당 데이터를 알면 안되기 때문
* MD5, SHA 알고리즘이 대표적
* 사용자 비밀번호 등을 저장할 때 자주 사용
* MD5와 SHA-0, SHA-1은 해시 충돌이 발생할 수 있는 취약점이 있어 사용 지양
* Rainbow Table을 통해 원문을 알아낼 수 있음
  * Rainbow Table: 평문과 해시 함수로 만든 문자열을 모두 저장시켜 놓은 표
  * 데이터를 탈취당하더라도, 원문을 알아낼 수 없도록 조치
  * Salt, Key stretching를 이용하여 해결
* Salt
  * 평문에 임의의 문자열을 추가하여 암호화
  * 128bit 이상으로 만들 것을 권장
  * 사용자마다 다른 Salt를 사용하게 하면 더 안전
* Key stretching
  * 해시를 여러 번 반복하여 원문을 알기 힘들게 만드는 방법
  * 일반적인 시스템에서 0.2초 이상 반복되면 안전
* Salt & Key stretching을 이용하는 알고리즘
  * 직접 구현보다 검증받은 알고리즘 사용이 안전
  * PBKDF2
  * bcrypt
    * 비밀번호 저장 목적



### 2. 양방향 암호화

* 평문을 복호화 할 수 있는 형태로 암호화하는 방법
* 대칭키 & 비대칭키 알고리즘으로 나뉨
  * 대칭키: AES
  * 비대칭키: RSA
* 대칭키 암호 알고리즘
  * AES(Advanced Encryption Standard)
  * **같은 키**를 이용하여 암호화, 복호화 가능
* 비대칭키 암호 알고리즘
  * RSA(Rivest, Shmir and Adleman)
  * **공개키, 개인키 두 가지 존재**
  * 소앤수 분해를 기반으로 만들어진 알고리즘
  * **HTTPS에서 사용**



### 3. JavaScript에서의 암호화

* crypto-js
  * bcrypt는 미구현





## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

