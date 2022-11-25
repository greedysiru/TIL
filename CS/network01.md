# 기초 JS, CS 상식 - 네트워크 기초



**본 내용은 프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript 강의를 토대로 작성하였습니다.**



## 브라우저에 URL을 입력한 이후의 과정

### Step1. URL 해성

* `scheme://<user>:<password>@<host>:<port>/<url-path>`
  * scheme: protocol이 들어가는 영역
  * 계정정보: 인증이 요구되는 경우, id, password를 입력하면 접속 허가를 받을 수 있음



### Step2. DNS 조회

* Domain Name System
* DNS는 도메인과 IP 주소를 서로 변환
* DNS로 요청을 보내기 전에, 브라우저 캐시와 hosts 파일을 참조
* DNS는 보통 통신사(ISP)에서 제공하는 것을 사용
* Name Server: DNS를 운영하는 서버
* URL 해석 -> 브라우저 캐시 확인 -> (없다면) hosts 파일 참조 -> (없다면) DNS 호출 -> Root Server -> TLD Server -> Authoritative Server -> IP 반환
* 서브 도메인이 붙는 경우는 전부 host



### Step3. 해당 IP가 존재하는 서버로 이동

* 해당 IP가 할당된 서버가 존재하는 대역으로 이동
* 네트워크 장비인 라우터를 통해 여러번 거친 후. 해당 서버가 존재하는 대역으로 접근



### Step4. ARP를 이용하여, MAC 주소 변환

* ARP: Address Resolution Protocol
* 논리 주소인 IP 주소를 물리 주소인 MAC 주소로 변환하는 프로토콜
* 실제 통신을 위해 변하지 않는 고유한 MAC 주소가 필요
* 네트워크 내에 ARP를 Broadcating하면, 해당 IP 주소를 가지고 있는 기기가 MAC 주소를 반환



#### IP 주소와 MAC 주소

* IP는 논리적인 주소
* MAC은 물리적인 주소
* 기계의 실제 위치를 알기 위해선 MAC 주소가 필요하다
* IP 주소: 논리적 주소
* MAC 주소: 물리적 주소
* IP는 대역을 통해 범위를 좁히는 용도로 사용
* 라우터: 물리적 위치를 알아내도록 도와줌



### Step5. TCP 통신을 통해 Socket을 염

* 네트워크를 통해 해당 기기로 패킷을 전달
* 3 way handshake로 연결을 요청
* 요청이 수락되면 기기는 패킷을 받아 처리



### Step6. 서버는 응답을 반환

* HTTP 프로토콜로 들어온 패킷을 읽고 처리
* 요청에 따른 적절한 응답 값을 반환



### Step7. 브라우저는 렌더링

* HTML을 읽어 DOM Tree를 구축
* 만들어진 DOM Tree를 이용하여 화면을 그림
* 스크립트를 실행



## Reference

[프로그래머스의 코딩테스트 광탈 방지 A to Z : JavaScript](https://school.programmers.co.kr/learn/courses/13213)

