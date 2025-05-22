---
date: '2025-05-22T20:00:31-03:00'
draft: false
title: 'Kafka Quick Commands'
---

This simple guide will explain how to kickstart with Kafka and do some simple commands.
Starting with how to up and running kafka in your computer, creating topic, publishing messages and consuming messages.

## Installation

TODO

### Creating a Topic

```bash
kafka-topics.sh --bootstrap-server localhost:9092 \
--create --topic firstTopic --partitions 1
```

#### Publishing a Message

#### Using `echo` and `jq` to compact the message

```bash
echo '{"name": "hello world"}' | jq -c | kafka-console-producer.sh \
--bootstrap-server localhost:9092 --topic firstTopic
```

#### From a file

```bash
kafka-console-producer.sh --bootstrap-server \
localhost:9092 --topic firstTopic < message.json
```

#### Consuming a Topic

```bash
kafka-console-consumer.sh --bootstrap-server \
localhost:9092 --topic firstTopic --from-beginning
```

#### Describing a Consumer Group

```bash
kafka-consumer-groups.sh --bootstrap-server \
localhost:9092 --group consumer_group_name --describe
```

#### Plan to Skip Offset

```bash
kafka-consumer-groups.sh --bootstrap-server \
localhost:9092 --group consumer_group_name --topic topic_0 \
--reset-offsets --shift-by 1
```

#### Execute Skip Offset

```bash
kafka-consumer-groups.sh --bootstrap-server \
localhost:9092 --group consumer_group_name --topic topic_0 \
--reset-offsets --shift-by 1 --execute
```

## Run Kafka UI

```bash
docker run -p 8080:8080 -e KAFKA_BROKERS=localhost:9092,192.168.0.1:9092 \
quay.io/cloudhut/kowl:master
```

> All commands are tested on Kafka 3.9.0
