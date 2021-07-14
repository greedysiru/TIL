# 면접 대비 예상 개념 정리


## JavaScript
* ECMA Script: 자바스크립트 표준

### JavaScript 엔진 동작
* 엔진: 소스 코드를 읽고 실행하는 부분
	 * 브라우저마다 자체 엔진이 있음
	 * Mozilla Firefox: Spidermonkey
	 * Edge: Chakra / ChakraCore
	 * Safari: JavaScriptCore
	 * Chrome: **V8** (Node.js의 엔진이기도 함) 
	 * V8: 자바스크립트의 상대적으로 느린 브라우저 인터프리팅을 대체
	
* 인터프리터와 컴파일러

   * 대부분의 엔진이 이 두 기술들을 사용
   * 인터프리터: 소스코드를 거의 즉시 실행
   * 컴파일러: 사용자의 시스템에서 직접 실행하는 기계 코드를 생성

   > **소스코드** -> **인터프리터** -> **자주 실행되는 코드** 부분을 **Hot path로 플래그 지정** -> 실행 중 수집 된 **컨텍스트 정보와 함께 컴파일러에 전달**

   엔진이 잘 실행되면, C++보다 우수한 특정 시나리오를 기대할 수 있음



## React

* 페이스북에서 만든 JavaScript 라이브러리
* 웹 애플리케이션 제작 시 뷰와 기능, 성능을 모두 챙길 수 있다.

## JSX

* React DOM 다룰 때 사용
  * DOM을 표현하는 다른 방식
* JavaScript 문법을 확장



## Babel

* JavaScript를 특정 JavaScript 버전으로 옮기는 역할(Transpiler)

## WebSocket
* 웹 브라우저와 서버 간에 소켓 연결을 설정하는 API 정의
	* 클라이언트와 서버 사이에 지속적인 연결이 설정되어 양측이 언제든지 데이터를 보낼 수 있음 
	* 새로운 URL 스키마를 사용
	* ws: HTTP 80 port, wss: HTTPS 443 port
* 핸드셰이크
	* WebScoket 연결을 설정
	* 클라이언트가 서버에 일반 HTTP 요청을 보내는 것으로 시작
	* 서버가 WebSocket 프로토콜을 지원하면, 업그레이드에 동의하여 응답 Upgrade 헤더를 통해 이를 알림
	* 연결 설정 시, open 이벤트가 클라이언트 측의  WebSocket 인스턴스에서 발생
