# 2024-05-25: WebSocket

WebSocket은 클라이언트와 서버 간의 양방향 통신을 가능하게 하는 프로토콜입니다. HTTP와 달리 지속적인 연결을 유지하며 실시간 데이터 전송에 적합합니다. WebSocket의 개념과 사용 방법은 다음과 같습니다.

## WebSocket

- **목적**: 클라이언트와 서버 간의 실시간 양방향 통신을 위해 사용됩니다.
- **특징**: 지속적인 연결 유지, 낮은 오버헤드, 실시간 데이터 전송에 최적화

## 주요 특징

1. **양방향 통신**: 클라이언트와 서버가 상호 간에 자유롭게 데이터를 주고받을 수 있습니다. 이는 채팅 애플리케이션, 실시간 알림 등에 유용합니다.
2. **지속적인 연결**: WebSocket 연결은 클라이언트와 서버가 처음 연결한 후 계속 유지되며, 재연결을 위한 추가 요청이 필요 없습니다.
3. **낮은 오버헤드**: WebSocket은 HTTP보다 헤더가 적어 데이터 전송 시 오버헤드가 낮습니다.
4. **실시간 데이터 전송**: 게임, 실시간 주식 시세, 스포츠 경기 결과 등 즉시 데이터 전송이 필요한 애플리케이션에 적합합니다.

## 사용 방법

### 서버 설정 (Java EE 사용)

먼저, Java 환경에서 WebSocket 서버를 설정하는 예제입니다.

```java
import javax.websocket.OnClose;
import javax.websocket.OnMessage;
import javax.websocket.OnOpen;
import javax.websocket.Session;
import javax.websocket.server.ServerEndpoint;
import java.io.IOException;

@ServerEndpoint("/websocket")
public class WebSocketServer {

    @OnOpen
    public void onOpen(Session session) throws IOException {
        System.out.println("New connection opened: " + session.getId());
        session.getBasicRemote().sendText("Hi there, I am a WebSocket server");
    }

    @OnMessage
    public void onMessage(String message, Session session) throws IOException {
        System.out.println("Received message: " + message);
        session.getBasicRemote().sendText("Hello, you sent -> " + message);
    }

    @OnClose
    public void onClose(Session session) throws IOException {
        System.out.println("Connection closed: " + session.getId());
    }
}

```

### 클라이언트 설정 예제

```java
import java.net.URI;
import javax.websocket.*;

@ClientEndpoint
public class WebSocketClient {

    @OnOpen
    public void onOpen(Session session) {
        System.out.println("Connected to server");
        try {
            session.getBasicRemote().sendText("Hello Server!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @OnMessage
    public void onMessage(String message) {
        System.out.println("Message from server: " + message);
    }

    @OnClose
    public void onClose(Session session) {
        System.out.println("Connection closed");
    }

    public static void main(String[] args) {
        WebSocketContainer container = ContainerProvider.getWebSocketContainer();
        try {
            URI uri = new URI("ws://localhost:8080/websocket");
            container.connectToServer(WebSocketClient.class, uri);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

## 주의사항
- **보안** : WebSocket은 보안이 중요한 애플리케이션에서는 wss:// 프로토콜을 사용하여 SSL/TLS를 적용하는 것이 좋습니다.
- **연결 관리** : 클라이언트나 서버가 연결을 해제하는 경우를 대비하여 적절한 예외 처리가 필요합니다.
- **부하 분산** : 다수의 클라이언트와 연결 시 서버의 부하를 고려하여 스케일링 방안을 마련해야 합니다.
## 요약
- **WebSocket** : 실시간 양방향 통신을 가능하게 하는 프로토콜로, 지속적인 연결을 유지하며 낮은 오버헤드로 실시간 데이터 전송에 최적화되어 있습니다.
**사용 방법** : Node.js와 웹 브라우저에서 WebSocket 서버와 클라이언트를 설정하는 방법을 예제로 제공했습니다.
**주의사항** : 보안, 연결 관리, 부하 분산에 주의해야 합니다.
