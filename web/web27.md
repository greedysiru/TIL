# SSL

**본 내용은 10분 테코톡 다니님의 강의를 토대로 작성하였습니다.**



## 1. SSL/TLS

* SSL의 업그레이드 버전이 TLS
  * 일반적으로는 동일한 의미로 사용
* 인증서를 무료로 발급해주는 서비스
  * Let's Encrypt
  * AWS Certificate Manager



### SSL

* Secure Sockets Layer
* Netscape Communications Corperation에서 웹 서버와 웹 브라우저 간의 보안을 위해 만든 프로토콜
* 인증기관과 사용자가 협력하기 때문에 안전한 접속 방법
  * 사용자가 접속하는 사이트가 믿을 수 있는 사이트인지 확인이 가능해짐
* 공개키/개인키 대칭키 기반으로 사용
  * 각 방식이 가진 단점 때문에 한 방식만 채택해서 사용하지 않음
  * 두 방식 적절히 섞어 사용



### 대칭키

* 동일한 키로 암호화와 복호화를 수행하는 방법
* 누구든지 암호화에 이용된 키를 가지고 있으면, 해당 데이터를 쉽게 복호화
* 해커가 대칭키를 가지고 있고, 데이터를 가로채면 해당 데이터 복호화가 가능
* 장점
  * 암호화와 복호화가 쉬움
* 단점
  * 키를 배송할 때 보안 이슈



### 공개키

* 서로 다른 키로 암호화, 복호화를 수행
* 비대칭키 방식으로도 불림
* 데이터 암호화 시에는 공개키를 사용하고 데이터 복호화 시에는 개인키를 사용
* 공개키로 암호화한 데이터는 오직 개인키로만 복호화할 수 있음
  * 누구든지 공개키를 가져도 상관이 없음
  * 공개키는 중간에 해커가 가로채도 문제가 되지 않음
* 장점
  * 보안상 더 안전함
* 단점
  * 공개키 방식은 대칭키 방식보다 암호화 연산 시간이 더 소요되어 비용이 더 큼



### SSL이 필요한 이유

* 서버와 브라우저간 전송되는 데이터를 외부의 공격자로부터 **보안**하기 위해 필요
* 암호화의 대상은 내용이 유출됐을 때 악용되어 사용될 수 있는 비밀번호, 개인 정보 등이 해당



## 2. SSL 통신 과정

* SSL은 공개키 방식과 대칭키 방식을 적절히 혼합해서 사용
* SSL은 공개키 방식으로 대칭키를 전달
* 대칭키를 활용하여 암호화와 복호화, 서버와 브라우저간 통신을 진행



### 통신 과정

* A에서 B로 접속 요청
* B는  A에게 공개키 전송
* A는 자신의 대칭키를 B에서 전달받은 B의 공개키로 암호화
* 암호화한 대칭키를 B에게 전달
* B는 A의 대칭키를 자신의 개인키로 복호화
* 복호화 결과로 A의 대칭키를 얻어냄
* 얻어낸 대칭키를 활용해서 A와 B는 안전하게 통신
* 즉, 데이터 암호화와 복호화를 위한 한 쪽의 대칭키를 다른 쪽의 공개키로 암호화하여 전송하면, 반대편에서 자신의 개인 키로 복호화하여 그 반대편의 대칭키를 알아내 이 대칭키를 바탕으로 서로 통신



### 인증기관 인증서 발급

* 사용자가 접속한 사이트가 유효한 사이트인지 확인
* 사이트는 사이트 인증서가 필요
  * 사이트 인증서는 인증기관에서 사이트에게 발급하는 문서
* 사이트에서 인증기관에게 사이트 정보화 사이트 공개키를 전달
* 인증기관에서는 사이트 인증서를 발급하기 전, 전달 받은 데이터를 검증
* 인증기관에서 성공적으로 검증을 완료하면, 인증 기관은 사이트 인증서를 생성하기 위해 이 데이터를 자신의 개인키로 서명
* 서명을 하고 나면, 사이트 인증서가 생성
* 인증서를 사이트에게 전달
* 인증기관은 사용자에게 자신의 공개키를 전달
* 사용자가 인증기관으로부터 전달받은 인증기관 공개키는, 사용자의 브라우저에 자동으로 내장



### 사용자 사이트 접속 요청 시

* 사용자가 사이트에 접속 요청
* 사이트는 자신이 신뢰할 수 있는 사이트임을 증명하기 위해 자신의 인증서 전달
* 사용자는 브라우저에 내장되어 있는 인증기관 공개키로 인증서를 복호화하여 검증
* 사이트 인증서를 해독하면, 사이트 정보와 공개키를 얻을 수 있음
* 얻은 사이트 공개키로 사용자는 자신의 대칭키를 암호화
* 암호화한 대칭키를 사이트에게 전달
* 사이트는 사용자로부터 전달받은 암호문을 해독하여 사용자의 대칭키를 얻음
* 얻은 대칭키를 활용하여 사용자와 사이트는 암호문을 주고 받을 수 있게 됨

# Reference

[[10분 테코톡] 다니의 HTTPS](https://www.youtube.com/watch?v=wPdH7lJ8jf0)

