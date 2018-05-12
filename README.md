# kafka Cheat Sheet

## Quickstart
* https://kafka.apache.org/quickstart

# Create and delete Kafka topic
```bash
kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 2 --partitions 10 --topic testtopic
kafka-topics.sh --delete --zookeeper localhost:2181 --topic testtopic
```

## Show existing Kafka topic configuration
```bash
# kafka-topics.sh --list --zookeeper localhost:2181
kafka-topics.sh --describe --zookeeper localhost:2181 --topic testtopic
```

## Modify number of partitions on Kafka topic
```bash
# kafka-topics.sh --alter --zookeeper localhost:2181 --partitions 10 --topic testtopic
```

## Modify number of replication-factor on Kafka topic
```bash
# cat testtopic.json
{
  "version":1,
  "partitions":[
    {"topic":"testtopic","partition":0,"replicas":[0,1]},
    {"topic":"testtopic","partition":1,"replicas":[0,1]},
    {"topic":"testtopic","partition":2,"replicas":[0,1]},
    {"topic":"testtopic","partition":3,"replicas":[0,1]},
    {"topic":"testtopic","partition":4,"replicas":[0,1]},
    {"topic":"testtopic","partition":5,"replicas":[0,1]},
    {"topic":"testtopic","partition":6,"replicas":[0,1]},
    {"topic":"testtopic","partition":7,"replicas":[0,1]},
    {"topic":"testtopic","partition":8,"replicas":[0,1]},
    {"topic":"testtopic","partition":9,"replicas":[0,1]}
  ]
}
# kafka-reassign-partitions.sh --zookeeper localhost:2181 --reassignment-json-file testtopic.json --execute
```

## Produce messages to Kafka topic
```bash
# kafka-console-producer.sh --broker-list localhost:9092 --topic testtopic < testtopic.txt
```

## Consume messages on Kafka topic
```bash
# kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic testtopic --from-beginning --property print.timestamp=true
```

## GELF example message
```json
{"version": "1.1", "level": 6, "timestamp": 1525762578.938, "_file": "/test.txt", "host": "test", "full_message": "test", "short_message": "test"}
```

## Show Kafka topic lag
```bash
# kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group logstash
```

## Add topic purge configuration
```bash
#kafka-configs.sh --zookeeper localhost:2181 --alter --entity-type topics --entity-name testtopic --add-config retention.ms=14400000,cleanup.policy=delete
```
