## 🌟 유저 인터페이스 구상  

### 1️⃣ 홈 화면 UI (전체 채팅방 목록)
<br/>

**🔹 엔드포인트 (URL 매핑): GetMapping("/") => 홈 경로로 지정**

**🔹 클라이언트 요청(JSON 형식): 없음**

**🔹 서버 응답 데이터(JSON 형식): ChatRoom(채팅방 목록)**

**🔹 렌더링될 HTML 파일: chatRoom.html**
<br/> <br/>

### 🚨 Repository 에서의 Iterable 반환형 변경시 문제 해결 🚨
<br/>

```java
public interface ChatRoomRepository extends CrudRepository<ChatRoom, Long> {
    List<ChatRoom> findAll(); // 명시적으로 List<T> 반환
}
```
<br/>

**🔹 공변 반환 타입을 통한 구체적인 하위 타입(List)로 변환**<br/><br/>

**🔍 공변 반환 타입이란?**

**부모 메서드를 오버라이딩할때 부모의 반환형(Iterator)보다 더 구체적인 타입으로 변환 가능한 것**

**🔹 Collection은 Iterator를 상속하고 List는 Collection 을 상속하므로 List는 Iterator를 간접적으로 구현한 것**

**🚨 findAll 메서드에 Not annotated method overrides method annotated with @NonNullApi 경고 발생🚨**

**🔹 이유 : findAll 메서드는 null 값을 반환하지 않으므로 메서드에 @Nonnull 어노테이션 추가 필요**

### 🌟 HTML 코드 작성(chatRoom.html) 

```javascript
<ul th:if="${not #lists.isEmpty(chatRooms)}">
        <li th:each="room : ${chatRooms}">
            <a th:href="@{/chat/room/{roomId}(roomId=${room.roomId})}" th:text="${room.title}"></a>
        </li>
    </ul>
</div>
``` 

**🔹 # 기호로 list 객체 처리 => thymeleaf 문법**

**🔹 th:each 문법으로 리스트 순회**

**🔹 $ : 서버(컨트롤러)에서 받은 chatRooms 객체 접근**


### =======================================

### 1️⃣-2 채팅방 개설 및 다른 클라이언트에 방 개설 실시간 전송

**🎯 동작 개요**

**🔹 1. 채팅방 개설 모달에서 POST "/createChatRoom" 경로로 ChatRoomDTO (title, memberId) 전달**

**🔹 2. 컨트롤러에서 채팅방 생성시 해당 정보를 "/topic/chatRooms" 구독자에게 전파**

```java
    // 채팅방 생성 API
    public String createRoom(ChatRoomDTO chatRoomDTO) {
        ChatRoom chatRoom = ChatRoom.fromDTO(chatRoomDTO);
        chatRoomRepository.save(chatRoom);

        // /topic/chatRooms 로 구독한 구독자들에게 새로 생긴 채팅방 전달
        messagingTemplate.convertAndSend("/topic/chatRooms", chatRoom);

        return "채팅방 개설 완료!";
    }

```

**🔹 개설된 채팅방을 DB에 저장 및 /topic/chatRooms 경로를 구독한 클라이언트(전체 자동 구독)에게 전파**



### 2️⃣ 채팅방 생성 UI 




### 3️⃣ 각 채팅방 UI(메세지, 방제목)