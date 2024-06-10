# 2024-05-15: PUT vs PATCH

PUT과 PATCH는 모두 HTTP 메서드로, 주로 웹 애플리케이션에서 리소스를 업데이트하는 데 사용됩니다. 이 둘의 주요 차이점은 다음과 같습니다.

## PUT

- **목적**: 전체 리소스를 업데이트하거나 새로 만듭니다.
- **동작 방식**: 클라이언트가 제공한 전체 리소스로 서버의 리소스를 대체합니다.
- **데이터 전송 방식**: 요청 본문에 전체 리소스를 포함해야 합니다.
- **멱등성**: 멱등성을 보장합니다. 동일한 PUT 요청을 여러 번 수행해도 결과는 동일합니다.
- **예시**: 
    ```http
    PUT /users/1
    Content-Type: application/json

    {
      "id": 1,
      "name": "John Doe",
      "email": "john.doe@example.com"
    }
    ```
    위의 예시에서 `PUT` 요청은 사용자 `1`의 전체 리소스를 업데이트합니다.

## PATCH

- **목적**: 리소스의 일부를 업데이트합니다.
- **동작 방식**: 클라이언트가 제공한 부분 리소스만 서버의 리소스에 적용됩니다.
- **데이터 전송 방식**: 요청 본문에 변경하고자 하는 필드만 포함합니다.
- **멱등성**: 멱등성을 보장하지 않습니다. 동일한 PATCH 요청을 여러 번 수행하면 결과가 다를 수 있습니다.
- **예시**:
    ```http
    PATCH /users/1
    Content-Type: application/json

    {
      "email": "new.email@example.com"
    }
    ```
    위의 예시에서 `PATCH` 요청은 사용자 `1`의 이메일만 업데이트합니다.

## 요약

| 구분   | PUT                                                                                         | PATCH                                                                     |
|--------|---------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| 목적   | 리소스 전체를 업데이트하거나 새로 만듭니다                                                   | 리소스의 일부를 업데이트합니다                                           |
| 데이터 전송 방식 | 전체 데이터를 전송                                                                  | 변경하고자 하는 부분만 전송                                              |
| 멱등성 | 멱등성을 보장 (동일한 요청을 여러 번 수행해도 결과가 동일)                                   | 멱등성을 보장하지 않음 (동일한 요청을 여러 번 수행하면 결과가 다를 수 있음) |
