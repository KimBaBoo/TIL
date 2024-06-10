# 2024-06-10: HTTP Headers

HTTP 헤더는 웹 서버와 클라이언트 간의 요청 및 응답 메시지에 포함된 추가 정보를 제공합니다. HTTP 헤더는 메시지의 본문(body)와 구분되며, 메타데이터 역할을 합니다. 헤더는 요청 헤더, 응답 헤더, 엔티티 헤더, 일반 헤더 등 다양한 종류가 있습니다.

## 1. HTTP 헤더의 기본 개념

- **설명**: HTTP 헤더는 클라이언트와 서버가 HTTP 메시지에 부가 정보를 포함하기 위해 사용됩니다. 메시지의 본문과는 구분되며, 메타데이터 역할을 합니다.

## 2. 헤더의 종류

- **일반 헤더**: 요청과 응답 모두에 적용되는 헤더로, `Date`, `Connection` 등이 있습니다.
- **요청 헤더**: 클라이언트가 서버로 요청을 보낼 때 사용하는 헤더로, `User-Agent`, `Accept` 등이 있습니다.
- **응답 헤더**: 서버가 클라이언트에 응답할 때 사용하는 헤더로, `Server`, `Set-Cookie` 등이 있습니다.
- **엔티티 헤더**: 요청과 응답 모두에 사용되며, 메시지 본문의 속성을 정의하는 헤더로, `Content-Length`, `Content-Type` 등이 있습니다.

## 3. 주요 HTTP 헤더 필드

- **Content-Type**: 본문의 MIME 타입을 지정합니다.
  - **예시**: `Content-Type: application/json`

- **Authorization**: 인증 정보를 포함합니다.
  - **예시**: `Authorization: Bearer token`

- **Cache-Control**: 캐싱 메커니즘을 제어합니다.
  - **예시**: `Cache-Control: no-cache`

- **User-Agent**: 클라이언트 소프트웨어 정보를 포함합니다.
  - **예시**: `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)`

- **Accept**: 클라이언트가 처리할 수 있는 콘텐츠 타입을 지정합니다.
  - **예시**: `Accept: text/html,application/xhtml+xml`

- **Set-Cookie**: 클라이언트에 쿠키를 설정합니다.
  - **예시**: `Set-Cookie: sessionId=abc123; Path=/; HttpOnly`

## 4. 실제 사용 예시

- **요청 헤더**:
## 4. 실제 사용 예시

- **요청 헤더**:
  ```yaml
  GET /index.html HTTP/1.1
  Host: www.example.com
  User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
  Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8
  ```

- **응답 헤더**:
  ```yaml
  HTTP/1.1 200 OK
  Date: Mon, 10 Jun 2024 12:00:00 GMT
  Server: Apache/2.4.1 (Unix)
  Content-Length: 438
  Content-Type: text/html
  Set-Cookie: sessionId=abc123; Path=/; HttpOnly
  ```

## 5. HTTP 헤더의 보안

- **설명**: 헤더를 통해 민감한 정보를 주고받을 때 보안에 유의해야 합니다. `Authorization` 헤더 사용 시 SSL/TLS를 통해 통신을 암호화하는 것이 중요합니다.
