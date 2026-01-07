## 실시간 채팅 구현

<br/>

### ◈ HTTP가 아닌 웹소켓(WebSocket)을 사용해야하는 이유 

- HTTP 통신은 클라이언트가 요청을 보내면 서버가 응답을 하는 수동적인 구조 
- 웹소켓은 서버가 클라이언트의 요청 없이 능동적으로 응답을 보낼 수 있음

<br/><br/>
### ◈ STOMP란

개념 : 웹소켓 위에서 동작하는 프로토콜(규칙)

* 발행(pub) / 구독(sub) 구조 

1. 구독 : 유저(A,B)가 토론방 1번 "/sub/chat/1"을 구독함
2. 발행 : 유저(C)가 토론방 1번 "/pub/chat/1"으로 메세지를 보냄
3. 브로커 : 유저 C가 보낸 메세지를 1번 방을 구독한 유저 A,B에게 C의 메세지를 뿌림.(Broadcast) 

<br/><br/>

----------------------------------------
<br/><br/>
## Spring 채팅 구현 순서 
<br/>

### 1. 의존성 추가 

- Websocket 사용 : Websocket dependency 추가 
- Stomp의 메세징 기능 : spring-messaging 추가 
- json <=> dto 자동 변환 : jackson-databind 추가 
- json 통역 : json-core(json) 추가 

### 2. WebSocketConfig 설정 

  - 클라이언트가 웹소켓 핸드셰이크를 하기 위해 연결할 endpoint 구현
  - 브로커의 pub / sub 의 prefix(주소) 설정

### 3. 채팅 구현을 위해 필요한 Entity 설정 

- 채팅방(ChatRoom) 및 채팅메세지(ChatMessage) 구현 

### 4. Controller 및 Service 로직 구현 

- 채팅방 개설, 메세지 보내기, 메세지 수신 로직 구현 
