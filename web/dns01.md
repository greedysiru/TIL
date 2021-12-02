# DNS(1)

**본 내용은 얄팍한 코딩사전님의 DNS가 뭔가요? + 도메인, A Record, CName 강의를 토대로 작성하였습니다.**



## DNS

* Domain Name System



### Domain

> www.siru.kr

* www 뒤에 붙는 것이 도메인
* www는 host name
* 웹 사이트에 접속할 때 IP대신 도메인으로 접근 가능



### DNS

* Domain과 IP를 저장해 놓는 곳
* 다층적으로 구성된 네트워크에 분산되어 도메인 정보들이 저장되고 조회



### 예시

* www.naver.com을 브라우저 주소창에 입력
* 브라우저가 PC에 설정된 로컬 DNS 서버에 해당 도메인과 호스트명의 IP를 가지고 있는 지 물어봄
  * 로컬 DNS서버는 통신사마다 지정된 곳이 있음
  * 사용자가 다른 곳으로 바꾸어 정부에서 막아놓은 사이트에 접속하거나 특정 서비스를 보다 빠르게 이용할 수 있음(다른 서비스는 느려질 수도 있음)
  * 주소의 정보가 캐싱되어있을 수도, 없을 수도 있음
* 가지고 있다면, 로컬 DNS는 바로 해당 도메인과 호스트명의 IP를 반환
* 가지고 있지 않다면, 로컬 DNS는 Root DNS 서버에다가 주소에 해당하는 IP를 어디서 찾을 수 있는지 물어봄
  * Root DNS 서버는 전세계에 13군데가 존재
* Root DNS 서버는 .com으로 끝나는 도메인들을 담당하는 서버의 IP 주소를 반환
* 로컬 DNS 서버는 해당 주소를 받아들이고 그곳을 찾아감
* .com 담당 서버는 naver.com의 도메인 정보를 가진 이 DNS 서버의 IP 주소를 반환
* 해당 주소를 보고 찾아가면 naver.com의 여러 호스트네임별 IP 주소들이 존재
* 여기로부터 www에 해당하는 IP주소를 얻어낸 다음 브라우저에게 반환
* www.naver.com으로 접속



### DNS Spoofing

* 사용자 컴퓨터가 DNS에 IP를 물어보는 시점에 가짜 사이트 IP를 알려주어 유도



# Reference

[[얄팍한 코딩사전] DNS가 뭔가요? + 도메인, A Record, CName](https://www.youtube.com/watch?v=6fc9NAQkcv0&t=10s)

