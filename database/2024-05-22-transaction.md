# 2024-05-22: SQL 트랜잭션

SQL 트랜잭션은 데이터베이스 관리 시스템에서 데이터 무결성을 보장하기 위해 사용되는 중요한 개념입니다. 트랜잭션은 여러 작업을 하나의 단위로 묶어 처리하며, 모든 작업이 성공적으로 완료되거나 모두 취소됩니다. SQL 트랜잭션의 주요 특징과 주의사항은 다음과 같습니다.

## SQL 트랜잭션

- **목적**: 데이터베이스 내에서 데이터 무결성을 보장하고, 일관성 있는 데이터 처리를 위해 사용됩니다.
- **ACID 속성**: 트랜잭션은 원자성(Atomicity), 일관성(Consistency), 고립성(Isolation), 지속성(Durability)을 준수합니다.
- **시작 및 종료**: 트랜잭션은 `BEGIN`, `COMMIT`, `ROLLBACK` 명령어로 시작하고 종료됩니다.

## 주요 특징

1. **원자성 (Atomicity)**: 트랜잭션 내의 모든 작업이 전부 수행되거나 전혀 수행되지 않아야 합니다. 하나의 작업이라도 실패하면 전체 트랜잭션이 취소됩니다.
2. **일관성 (Consistency)**: 트랜잭션이 성공적으로 완료되면 데이터베이스는 일관성 있는 상태를 유지해야 합니다. 모든 데이터 무결성 제약 조건이 준수되어야 합니다.
3. **고립성 (Isolation)**: 트랜잭션이 실행되는 동안 다른 트랜잭션의 영향을 받지 않아야 합니다. 각 트랜잭션은 독립적으로 실행됩니다.
4. **지속성 (Durability)**: 트랜잭션이 성공적으로 완료되면 그 결과는 영구적으로 반영되어야 합니다. 시스템 오류가 발생하더라도 데이터는 손실되지 않습니다.

## 주의사항

- **교착 상태**: 여러 트랜잭션이 동일한 자원을 동시에 요청할 때 교착 상태가 발생할 수 있습니다. 이를 방지하기 위해 적절한 락(lock) 전략과 타임아웃 설정이 필요합니다.
- **복구 전략**: 트랜잭션 실패 시 데이터베이스를 복구할 수 있는 전략이 필요합니다. 주로 로그 파일을 통해 복구합니다.
- **성능 문제**: 트랜잭션은 데이터베이스 성능에 영향을 줄 수 있습니다. 따라서 적절한 트랜잭션 크기와 실행 시간을 고려해야 합니다.

## 예시

### 트랜잭션 사용 예제

```
BEGIN;

UPDATE accounts SET balance = balance - 1000 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 1000 WHERE account_id = 2;

COMMIT;
```

위 예제는 ID가 1인 계좌에서 1000원을 인출하고, ID가 2인 계좌에 1000원을 입금하는 트랜잭션입니다.

```
BEGIN;

UPDATE accounts SET balance = balance - 1000 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 1000 WHERE account_id = 2;

ROLLBACK;
```

위 예제는 동일한 작업을 수행하지만, ROLLBACK 명령어로 인해 모든 변경 사항이 취소됩니다.

요약
- **트랜잭션**: 데이터베이스 내에서 데이터 무결성을 보장하기 위해 여러 작업을 하나의 단위로 묶어 처리합니다. 트랜잭션은 원자성, 일관성, 고립성, 지속성을 준수합니다.
- **주의사항**: 교착 상태를 방지하고, 복구 전략을 마련하며, 성능 문제를 고려해야 합니다.
- **예시**: BEGIN, COMMIT, ROLLBACK 명령어를 사용하여 트랜잭션을 관리합니다.