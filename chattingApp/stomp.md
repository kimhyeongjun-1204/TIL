## 📌 STOMP란? 

### 🔹 개념 : **웹소켓** 위에서 동작하는 문자 기반의 메세징 프로토콜. 

### 🔹 기본적으로 pub / sub 구조임. 

> ### 💡 pub / sub 구조란 ? 
> 발행자(publisher)와 구독자(subscriber) 간의 비동기적인 메시지 통신을 처리하는 패턴.  
> 🔹 발행자 : 메세지를 발행하는 주체 <br/><br/>
> 🔹 구독자 : 보낸 메세지를 받는 주체. <br/>        구독자는 특정 주제를 구독하여 그 주체에 발행된 메세지를 받음 <br/><br/>
> 🔹 메세지 브로커 : 발행자와 구독자 간의 중개 역할을 하는 시스템.  

## 🎯 Pub / Sub 패턴의 흐름

### 1️⃣ Publisher는 메세지를 Topic에 발행.

### 2️⃣ Subscriber는 관심 있는 Topic을 구독하고 해당 Topic에 메세지가 발행되면 이를 자동으로 수신. 

### 3️⃣ Message Broker는 발행된 메세지를 각 구독자에게 전달함. 

## 🎯 WebSocketConfig에서 STOMP 경로 설정 및 클라이언트 소켓 연결(핸드쉐이크) 경로 설정하기 

```bash
    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableSimpleBroker("/room"); # 메시지를 브로드캐스트할 경로
        registry.setApplicationDestinationPrefixes("/send"); # 메시지를 보내는 경로
    }
``` 

### 🔹 "/topic" 경로 => 발행자(Publisher)가 구독자(Subscriber)에게 받은 메세지를 브로드캐스팅함. 
### 🔹 "/app" 경로 => 구독자가 발행자에게 메세지 전달 


```bash
    @MessageMapping("/{roomId}") //  /send/{roomId} 경로로 클라이언트(구독자)의 메세지가 들어오면 다른 구독자들에게 브로드캐스팅하는 메소드가 실행됨
    @SendTo("/room/{roomId}") // /room/{roomId} 경로를 구독한 클라이언트에 메세지 전달
    public ChatMessage chat(@DestinationVariable Long roomId, ChatMessageDto chatMessageDto) {
        return chatMessageService.sendMessage(chatMessageDto);
    }
```

### 🎯 클라이언트가 /send/{roomId} 경로로 메세지를 전달하면 다른 구독자들에게 이를 전달하는 메소드 
### 🔹 서버에 메세지(ChatRoomDto)가 들어옴 => 서버가 DB에 저장 => roomId를 구독한 다른 클라이언트에게 메세지 브로드캐스팅(@SendTo) 


