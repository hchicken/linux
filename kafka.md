# kafka

[__TOC__]

## 介绍

> Apache Kafka是一个分布式消息发布订阅系统。它最初由LinkedIn公司基于独特的设计实现为一个分布式的提交日志系统( a distributed commit log)，，之后成为Apache项目的一部分。Kafka系统快速、可扩展并且可持久化。它的分区特性，可复制和可容错都是其不错的特性。

## 与其他消息系统对比

* 分布式系统，易于向外扩展
* 同时为发布和订阅提供高吞吐量
* 支持多订阅者，当失败时能自动平衡消费者
* 可将消息持久化到磁盘，因此可用于批量消费，例如ETL，以及实时应用程序

## 基本结构

### Topic

* Kafka将消息种子(Feed)分门别类， 每一类的消息称之为话题(Topic)

### Producer

* 发布消息的对象称之为话题生产者(Kafka topic producer)

### Consumer

* 订阅消息并处理发布的消息的种子的对象称之为话题消费者(consumers)

### Broker

* 已发布的消息保存在一组服务器中，称之为Kafka集群。集群中的每一个服务器都是一个代理(Broker). 消费者可以订阅一个或多个话题，并从Broker拉数据，从而消费这些已发布的消息。

## kafka安装

### kafak/zookeeper镜像拉取

```bash
docker pull wurstmeister/zookeeper  
docker pull wurstmeister/kafka
```

### 启动zk

```
docker run -d --name zookeeper -p 2181:2181 -t wurstmeister/zookeeper
```

### 启动kafka

```bash
docker run  -d --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=x.x.x.x:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://x.x.x.x:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka
```