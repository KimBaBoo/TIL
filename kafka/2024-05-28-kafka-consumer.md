# 2024-05-28: Kafka Consumer

Kafka Consumer는 Apache Kafka 메시지 브로커 시스템에서 데이터를 수신하여 처리하는 역할을 합니다. 분산형 데이터 스트리밍 플랫폼인 Kafka에서 컨슈머는 특정 토픽으로부터 데이터를 읽어와 처리합니다. Kafka Consumer의 개념과 사용 방법은 다음과 같습니다.

## Kafka Consumer

- **목적**: Kafka 토픽에서 데이터를 읽어와 처리하는 역할을 합니다.
- **특징**: 고성능, 확장성, 신뢰성 있는 데이터 처리를 지원합니다.

## 주요 특징

1. **고성능 데이터 처리**: 대량의 데이터를 고속으로 처리할 수 있습니다. 이는 실시간 데이터 분석, 로그 처리 등에 유용합니다.
2. **확장성**: 분산형 구조로 쉽게 확장할 수 있어, 데이터 양의 증가에도 유연하게 대응할 수 있습니다.
3. **신뢰성**: 데이터 처리를 신뢰성 있게 보장하며, 처리 실패 시 자동으로 재시도합니다.
4. **오프셋 관리**: Kafka는 컨슈머 오프셋을 관리하여 데이터의 정확한 처리를 보장합니다.

## 사용 방법

### 컨슈머 설정 (Java 사용)

```java
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import java.util.Collections;
import java.util.Properties;

public class SimpleConsumer {
    public static void main(String[] args) {
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");
        props.put("group.id", "test-group");
        props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
        consumer.subscribe(Collections.singletonList("my-topic"));

        try {
            while (true) {
                ConsumerRecords<String, String> records = consumer.poll(100);
                for (ConsumerRecord<String, String> record : records) {
                    System.out.printf("offset = %d, key = %s, value = %s%n", record.offset(), record.key(), record.value());
                }
            }
        } finally {
            consumer.close();
        }
    }
}
```

## 주의사항
- **보안** : Kafka는 기본적으로 보안이 설정되어 있지 않으므로, 민감한 데이터를 전송할 경우 SSL/TLS 설정이 필요합니다.
- **연결 관리** : 컨슈머가 정상적으로 종료될 수 있도록 close 메서드를 호출하여 리소스를 정리해야 합니다.
- **오프셋 관리** : 컨슈머 오프셋을 주기적으로 커밋하여 데이터 손실을 방지해야 합니다.
- **오류 처리** : 데이터 처리 중 발생할 수 있는 오류를 처리하기 위해 적절한 예외 처리가 필요합니다.
- **성능 최적화** : 비동기 데이터 처리와 배치 처리를 활용하여 성능을 최적화할 수 있습니다.
## 요약
- **Kafka Consumer** : Kafka 토픽에서 데이터를 읽어와 처리하는 역할을 합니다.
- **사용 방법** : Java 환경에서 Kafka Consumer를 설정하는 예제를 제공했습니다.
- **주의사항** : 보안 설정, 연결 관리, 오프셋 관리, 오류 처리, 성능 최적화에 주의해야 합니다.
