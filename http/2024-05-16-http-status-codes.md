# 2024-05-16: http-status-code

## HTTP 응답 코드

### 1xx: 정보 응답 (Informational)
- **100 Continue**: 요청의 일부를 수신했고, 나머지를 계속 보내도 됩니다.
- **101 Switching Protocols**: 서버가 클라이언트의 프로토콜 전환 요청을 수락했습니다.
- **102 Processing (WebDAV)**: 요청을 수신하였으며, 서버가 요청을 처리하고 있음을 나타냅니다.

### 2xx: 성공 응답 (Success)
- **200 OK**: 요청이 성공적으로 완료되었습니다.
- **201 Created**: 요청이 성공적으로 완료되었으며, 새로운 리소스가 생성되었습니다.
- **202 Accepted**: 요청을 수신하였으나, 처리가 완료되지 않았습니다.
- **204 No Content**: 요청이 성공적으로 처리되었지만, 반환할 콘텐츠가 없습니다.

### 3xx: 리다이렉션 응답 (Redirection)
- **301 Moved Permanently**: 요청한 리소스가 영구적으로 새로운 URI로 이동되었습니다.
- **302 Found**: 요청한 리소스가 임시로 다른 URI에 있습니다.
- **303 See Other**: 요청한 리소스를 다른 URI에서 GET 메소드를 통해 얻으라는 응답입니다.
- **304 Not Modified**: 클라이언트의 조건부 요청에 대해 리소스가 수정되지 않았음을 나타냅니다.

### 4xx: 클라이언트 오류 응답 (Client Error)
- **400 Bad Request**: 서버가 잘못된 요청을 이해할 수 없습니다.
- **401 Unauthorized**: 인증이 필요합니다.
- **403 Forbidden**: 서버가 요청을 거부하였습니다.
- **404 Not Found**: 요청한 리소스를 찾을 수 없습니다.
- **405 Method Not Allowed**: 요청한 메소드는 서버에서 허용되지 않습니다.
- **409 Conflict**: 요청이 리소스의 현재 상태와 충돌이 발생했습니다.
- **429 Too Many Requests**: 클라이언트가 일정 시간 내에 너무 많은 요청을 보냈습니다.

### 5xx: 서버 오류 응답 (Server Error)
- **500 Internal Server Error**: 서버에서 오류가 발생하여 요청을 수행할 수 없습니다.
- **501 Not Implemented**: 서버가 요청된 기능을 지원하지 않습니다.
- **502 Bad Gateway**: 게이트웨이 또는 프록시 서버가 상위 서버로부터 잘못된 응답을 받았습니다.
- **503 Service Unavailable**: 서버가 일시적으로 사용 불가능합니다.
- **504 Gateway Timeout**: 게이트웨이 또는 프록시 서버가 상위 서버로부터 응답을 받지 못했습니다.
