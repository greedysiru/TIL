# HTTP vs. HTTPS

**본 내용은 10분 테코톡 다니님의 강의를 토대로 작성하였습니다.**



## 1. HTTP 
* Hypertext Transfer Protocol
* 서로 다른 시스템들 사이에서 통신을 주고받게 하는 가장 기본적인 프로토콜
* 서버에서 브라우저로 데이터를 전송하는 용도로 가장 많이 사용
* **문제점**
  * 서버에서 브라우저로 전송되는 정보가 암호화되지 않음
  * 데이터가 쉽게 도난당할 수 있음



## 2. HTTPS

* Hypertext Transfer Protocol Secure
* SSL(보안 소켓 계층) 사용
* SSL
  * 서버와 브라우저 사이에 안전하게 암호화된 연결을 만들 수 있게 도와줌
  * 서버와 브라우저가 민감한 정보를 주고받을 때 해당 정보가 도난 당하는 것을 막아줌
* HTTP 자체를 암호화하는 것은 아님
* HTTP를 사용해서 운반하는 내용(HTTP Message Body)를 암호화
  * HTTP Header는 암호화가 되지 않음



## 3. HTTPS를 사용해야 하는 이유

### 보안성

* HTTP로 데이터를 전송하는 경우, 네트워크로 전달되는 데이터는 원본 그 자체
* 해커가 중간에서 가로챈 후, 데이터의 내용을 알 수 있음
* HTTPS로 데이터를 전송하는 경우, 네트워크로 전달되는 데이터는 암호화 됨
* 해커가 중간에서 가로채도 데이터의 내용을 알 수 없음



### SEO

* 검색 엔진 최적화
* HTTPS 사이트의 경우, 구글이 해당 웹 사이트에 가산점을 줌
* AMP(가속화된 모바일 페이지)를 만들 때 HTTPS를 사용해야만 함

# Reference

[[10분 테코톡] 다니의 HTTPS](https://www.youtube.com/watch?v=wPdH7lJ8jf0)