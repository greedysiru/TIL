# TCP/IP

**본 내용은 10분 테코톡 수리님의 강의를 토대로 작성하였습니다.**



## 1. 인터넷

* 전 세계에 걸쳐 파일 전송 등의 데이터 통신 서비스를 받을 수 있는 컴퓨터 네트워크의 시스템
* 인터넷을 사용한다는 것은 사업자가 만들어 놓은 네트워크 인프라를 사용하는 것
  * 사업자가 만들어 놓은 자가망은 해저 광속 케이블을 통해 해외 네트워크 망과 연결되어 있음
* 데이터를 디지털 신호로 바꾸어 전달하고 받은 디지털 신호를 다시 데이터를 바꾸어가며 네트워크 통신이 이루어짐
* **네트워크 통신을 위해 미리 정해놓은 공통된 메뉴얼을 프로토콜이라고 함**



## 2. TCP/IP

### TCP/IP란

* 인터넷에서 컴퓨터들이 서로 정보를 주고 받는데 쓰이는 프로토콜의 집합



### TCP/IP의 계층

* Application Layer
  * 특정 서비스를 제공하기 위해 애플리케이션 끼리 정보를 주고 받을 수 있음
  * FTP, HTTP, SSH, Telnet, DNS, SMTP
  * ex) 브라우저와 웹서버가 HTTP 요청, 응답을 통해 통신
* Transport Layer
  * 송신된 데이터를 수신측 애플리케이션에 확실히 전달하게 함
  * TCP, UDP, RTP, RTCP
  * 포트번호를 사용해서 애플리케이션을 찾아 주는 역할을 함
* Internet Layer
  * 수신 측 까지 데이터를 전달하기 위해 사용
  * 송신측, 수신측 모두 IP주소를 가지고 있음
  * IP주소를 바탕으로 올바른 목적지로 찾아 갈 수 있도록 함
  * IP, ARP, ICMP, RARP, OSPF
* Network Access Layer
  * 네트워크에 직접 연결된 기기 간 전송을 할 수 있도록 함
  * 물리적 주소인 MAC 주소를 사용
  * Ethernet, PPP, Token Ring



## 3. TCP/IP 흐름

> 웹 브라우저에 www.google.com을 입력하면 일어나는 일

* google 웹서버의 80포트로 HTTP Request 메시지를 보냄
* 해당 요청을 인터넷을 통해 구글서버로 전달하기 위해 패킷을 만들어야 함
* 패킷에는 각 계층에 필요한 정보들이 담겨야 함

| 계층     | Network Access Layer | Internet Layer | Transport Layer | Application Layer |
| -------- | :------------------: | :------------: | :-------------: | :---------------: |
| **패킷** |       Ethernet       |       IP       |       TCP       |       HTTP        |



### TCP Packet

* SP: 시작 포트번호
  * 요청 컴퓨터에서 만든 소켓의 포트 번호
* DP: 목적지 포트번호
  * 80포트: 웹 서버의 웰노운 포트 번호
* 연결지향형 프로토콜
  * **3-way-handshaking**: 데이터를 전송하기 전에, 송신측과 수신측이 연결되는 작업이 필요
  * 헤더에 컨트롤비트라는 플래그들(SYN, ACK) 이 필요



### IPv4 Packet

* SA: 시작 IP 주소
* DA: 목적지 IP 주소
  * DNS 프로토콜을 통해서 도메인정보로부터 IP주소를 알아낼 수 있음



### DNS Server

* 브라우저는 OS에게 도메인에대한 IP주소를 요청
* OS는 DNS서버로 요청
  * 도메인이 담긴 쿼리를 도메인 서버로 보냄
  * 이에대해 도메인 서버가 IP 주소를 응답
* DNS서버 주소는 이미 컴퓨터에 등록되어 있음
* DNS도 Application Layer의 프로토콜
  * 53번 포트를 사용
* Transport Layer에서 UDP 프로토콜 사용
  * UDP는 포트번호만 있는 프로토콜
  * 비연결지향형 프로토콜



### Ethernet 프로토콜

* 헤더를 만들기위해 MAC주소가 필요
* 물리적으로 연결된 공유기의 MAC 주소가 필요
  * 공유기를 통해 다른 네트워크와 연결이 가능하므로 게이트웨이라고도 함
  * Network Address Tranlation(NAT): 공유기가 Private IP를 Public IP로 전환
* ARP프로토콜을 통해 MAC주소를 알아냄
  * IP주소를 MAC주소로 바꾸어주는 주소해석 프로토콜



### 3-Way-Handshaking

* 데이터를 전송하기 전에, 송신측과 수신측이 연결되는 작업
* TCP 헤더에 컨트롤 비트라는 플래그들(SYN, ACK) 필요
* 클라이언트는 서버에게 접속을 요청하는 SYN 패킷을 보냄
* 서버는 SYN 요청을 받고 클라이언트에게 요청을 수락한다는 ACK과 SYN 플래그가 설정된 패킷을 보냄
* 클라이언트는 서버에게 다시 ACK을 보냄
* 그 이후로, 연결이 이루어지고 데이터가 오가게 됨(연결 성립)



### Routing

* 목적지 서버에 도착하기 위해 여러 라우터를 거침
* 라우터는 네트워크와 네트워크를 연결해주는 역할
* 목적지 서버가 연결된 라우터에 데이터가 도착하면, 패킷의 IP헤더에 기록된 구글 서버 IP주소를 통해 MAC 주소를 얻어와야 함(ARP 프로토콜 사용)
  * ARP 프로토콜은 라우터가 연결된 네트워크에 브로드캐스팅 됨
  * 목적지 서버가 자신의 IP로 온 ARP 요청을 받고 MAC 주소를 응답
  * 이후, 데이터가 물리적으로 전달 가능



### Transport Layer 

* 목적지 포트 번호에는 80번이 적혀 있음
* 80번 포트를 사용하고 있는 애플리케이션에게 데이터를 전달



### Application Layer

* 웹 서버가 사용될 HTTP Request 데이터를 얻을 수 있게 됨



### 4-Way-Handshaking

* HTTP 요청과 응답과정이 끝나면 연결을 종료
* TCP 컨트롤 비트 사용
  * ACK, FIN 플래그 사용
* 클라이언트가 서버로 연결을 종료하겠다는 FIN 플래그 전송
* 서버는 클라이언트에게 ACK 메시지를 보내고 자신의 통신이 끝날 때까지 기다림
* 서버가 통신이 끝나면 클라이언트로 FIN을 보냄
  * 서버가 FIN을 보내기 전에 보냈던 데이터가 FIN보다 늦게 도착할 수도 있음
  * TIME_WAIT: 이를 대비하여 클라이언트는 FIN을 받고 일정시간동안 소켓을 닫지 않음
* 클라이언트는 확인의 의미로 서버에게 ACK를 보냄
* 연결 종료 완료



## 4. 신뢰할 수 있는 TCP

* 큰 데이터를 한 개의 패킷으로 주고받기에는 무리가 있음
* 데이터를 잘게 쪼개서 많은 패킷에 보내게 됨
* 이러한 패킷들은 복잡한 인터넷을 통해 목적지로 이동
* TCP는 이런 복잡한 환경에서 데이터를 유실 없이 올바른 순서대로 도착할 수 있게 함
  * 신뢰성있는 데이터 전송 보장
  * 흐름제어
  * 오류제어
  * 혼잡제어



# Reference

[[10분 테코톡] 수리의 TCP/IP](https://www.youtube.com/watch?v=BEK354TRgZ8)