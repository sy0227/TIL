# SockJS, Stomp를 통한 WebSocket 구현

### WebSocket이란?
웹소켓(WebSocket)은 하나의 TCP 접속에 전이중 통신 채널을 제공하는 컴퓨터 통신 프로토콜이다. 웹소켓 프로토콜은 2011년 IETF에 의해 RFC 6455로 표준화되었으며 웹 IDL의 웹소켓 API는 W3C에 의해 W3C 차세대 웹 표준기술로 확정되었다.

#### WebSocket Overview
WebSocket 프로토콜은 클라이언트와 서버간에 지속적인 양방향 통신을 설정하기 위해 HTTP 1.1 프로토콜로 확장한다.
1. 클라이언트와 서버간에 통신 채널을 설정하려면 클라이언트가 서버로 HTTP 업그레이드 요청을 보내야한다. 이를 WebSocket 프로토콜 핸드 셰이크라고한다.
2. 만약 서버가 연결을 업그레이드 할 수 있는 경우, HTTP 101 응답을 요청한 클라이언트에 보낸다. 이 시점에서 핸드 셰이크가 성공한 것으로 간주되고 서버와 클라이언트 간의 연결이 WebSocket 프로토콜로 업그레이드된다.
(참고 : 클라이언트가 HTTP 101 응답을받는 즉시, 연결은 더 이상 HTTP와 연결되었다고 간주되지 않는다.)
3. 이제 메시지는 WebSocket 연결을 통해 서버와 클라이언트간에 양방향으로 흐를 수 있다.
4. 데이터 교환에 참여한 모든 참가자(Websocket 연결된 사람)는 다른 참가자에게 닫기 요청을 전송하여 WebSocket 연결을 종료하도록 요청할 수 있다.

#### Spring Stomp Schema
![Spring Stomp Schema](https://t1.daumcdn.net/cfile/tistory/21423C3958E9D4950E)
  
#### Socket.io
Node.js 기반으로 만들어진 기술로 자체 스팩으로 만들어진 socket.io 서버를 만들고 socket.io 클라이언트와 브라우저에 구애받지 않고 실시간 통신이 가능해진다. socket.io는 node.js 기반이기 때문에 모든 코드가 javascript로 작성되어 있다. 서버, 클라이언트 모두 javascript 기반으로 개발하는 것이 기본이다.

#### SockJS
Spring framework에서 WebSocket을 지원한다. 스프링 메뉴얼에 WebSocket 부분을 보면 위와 같은 브라우저 문제를 해결하기 위한 방법으로 SockJS를 솔루션으로 제시한다. 역시 자체 스펙으로 WebSocket 미지원 브라우저를 관리한다. 서버 개발 시 스프링 설정에서 일반 WebSocket 으로 통신할지 SockJS 호환으로 통신할지 결정할 수 있다. 클라이언트쪽은SockJS client를 통해 서버와 통신한다.  

##### 출처
[Stomp와 SockJs를 통한 WebSocket 구현하기](https://postitforhooney.tistory.com/entry/SpringStomp-Spring-stomp%EC%99%80-Socjks%EB%A5%BC-%ED%86%B5%ED%95%9C-%EC%9B%B9%EC%86%8C%EC%BC%93-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%9E%A5%EB%8B%A8%EC%A0%90)
