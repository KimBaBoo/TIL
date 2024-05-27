# 2024-05-27: Kafka Broker

Kafka Broker는 Apache Kafka 메시지 브로커 시스템에서 핵심적인 역할을 수행합니다. 분산형 데이터 스트리밍 플랫폼인 Kafka에서 브로커는 메시지의 저장과 관리, 프로듀서와 컨슈머 간의 데이터 전송을 담당합니다. Kafka Broker의 개념과 특징은 다음과 같습니다.

## Kafka Broker

- **목적**: 메시지를 저장하고 관리하며, 프로듀서와 컨슈머 간의 데이터 전송을 담당합니다.
- **특징**: 고성능, 확장성, 고가용성, 신뢰성 있는 메시지 관리를 지원합니다.

## 주요 특징

1. **고성능 데이터 처리**: 대량의 데이터를 효율적으로 저장하고 처리할 수 있습니다. 이는 실시간 데이터 스트리밍과 로그 수집 등에 유용합니다.
2. **확장성**: 브로커는 클러스터 내에서 쉽게 확장할 수 있어, 데이터 양의 증가와 시스템 부하에 유연하게 대응할 수 있습니다.
3. **고가용성**: 다수의 브로커를 통해 데이터의 복제 및 분산 저장을 지원하여 시스템 장애 시에도 데이터 손실을 최소화합니다.
4. **신뢰성**: 메시지의 신뢰성을 보장하며, 데이터 손실이나 중복을 방지하기 위한 다양한 메커니즘을 제공합니다.

## 구성 요소

1. **메시지 로그**: 브로커는 토픽의 각 파티션에 메시지를 로그 형태로 저장합니다.
2. **파티션**: 각 토픽은 여러 파티션으로 나뉘며, 각 파티션은 특정 브로커에 저장됩니다.
3. **리플리케이션**: 데이터의 복제를 통해 고가용성을 확보합니다. 각 파티션은 여러 브로커에 복제될 수 있습니다.
4. **컨트롤러**: 클러스터 내에서 브로커의 상태를 관리하고, 리더 선출 등의 중요한 작업을 수행합니다.

## 브로커 클러스터

Kafka는 일반적으로 다수의 브로커로 구성된 클러스터 형태로 운영됩니다. 클러스터 내에서 각 브로커는 다음과 같은 역할을 수행합니다:

1. **리더(Leader)**: 각 파티션의 리더는 모든 읽기 및 쓰기 요청을 처리합니다. 리더는 클러스터 내의 한 브로커에 할당됩니다.
2. **팔로워(Follower)**: 팔로워는 리더의 데이터를 복제하며, 리더가 장애를 겪을 경우 새로운 리더로 승격될 수 있습니다.

## 사용 방법

### 브로커 설정 (예시)

Kafka Broker를 설정하는 기본적인 예시는 다음과 같습니다. 설정 파일은 `server.properties`로 저장됩니다.

```properties
# 브로커 1 설정 (server-1.properties)
broker.id=1
log.dirs=/var/lib/kafka/logs1
zookeeper.connect=localhost:2181
port=9092
# 클러스터 내의 다른 브로커들과 동일하게 설정
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
default.replication.factor=3
replica.fetch.max.bytes=1048576
```
```properties
# 브로커 2 설정 (server-2.properties)
broker.id=2
log.dirs=/var/lib/kafka/logs2
zookeeper.connect=localhost:2181
port=9093
# 클러스터 내의 다른 브로커들과 동일하게 설정
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
default.replication.factor=3
replica.fetch.max.bytes=1048576
```
```properties
# 브로커 3 설정 (server-3.properties)
broker.id=3
log.dirs=/var/lib/kafka/logs3
zookeeper.connect=localhost:2181
port=9094
# 클러스터 내의 다른 브로커들과 동일하게 설정
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
default.replication.factor=3
replica.fetch.max.bytes=1048576
```

브로커 설정 후, Kafka Broker를 시작하는 명령어는 다음과 같습니다.

```sh
bin/kafka-server-start.sh config/server-1.properties
bin/kafka-server-start.sh config/server-2.properties
bin/kafka-server-start.sh config/server-3.properties
```

### 설명
- **broker.id** : 각 브로커의 고유 ID입니다. 클러스터 내에서 유일해야 합니다.
- **log.dirs** : 각 브로커가 로그를 저장할 디렉토리 경로입니다.
- **zookeeper.connect** : 주키퍼 서버의 주소입니다. 모든 브로커가 동일한 주키퍼 클러스터에 연결되어야 합니다.
- **port**: 각 브로커가 사용하는 포트입니다. 각 브로커는 고유한 포트를 사용해야 합니다.
- **default.replication.factor** : 기본 복제 계수로, 각 파티션이 몇 개의 브로커에 복제될지를 설정합니다. 3대의 브로커를 운영하는 경우 복제 계수는 3으로 설정하는 것이 일반적입니다.
- **replica.fetch.max.bytes** : 팔로워 브로커가 리더 브로커로부터 데이터를 가져올 때의 최대 크기입니다.


## 주의사항
- **보안** : Kafka는 기본적으로 보안이 설정되어 있지 않으므로, 민감한 데이터를 전송할 경우 SSL/TLS 설정이 필요합니다.
- **모니터링** : 브로커의 상태와 성능을 모니터링하기 위해 Kafka 관리 도구를 사용하여 실시간으로 상태를 체크해야 합니다.
- **데이터 유지** : 로그 세그먼트의 보관 주기를 설정하여 오래된 데이터를 자동으로 삭제하도록 구성할 수 있습니다.
- **장애 복구** : 브로커 장애 시 데이터 복구 계획을 마련하여 데이터 손실을 최소화해야 합니다.

## 요약
- **Kafka Broker** : 메시지를 저장하고 관리하며, 프로듀서와 컨슈머 간의 데이터 전송을 담당합니다.
- **브로커 클러스터** : 다수의 브로커를 통해 고가용성과 확장성을 제공하며, 리더와 팔로워의 역할을 통해 안정성을 유지합니다.
- **사용 방법** : 브로커 설정과 시작 방법을 예시로 제공했습니다.
- **주의사항** : 보안 설정, 모니터링, 데이터 유지 및 장애 복구에 주의해야 합니다.
