---
layout:     post
title:      KAFKA
tags:		KAFKA
---
参考：http://blog.csdn.net/suifeng3051/article/details/48053965

kafka-即是解决上述这类问题的一个框架，它实现了生产者和消费者之间的无缝连接。
kafka-高产出的分布式消息系统(A high-throughput distributed messaging system)
Apache kafka 是一个分布式的基于push-subscribe的消息系统，它具备快速、可扩展、可持久化的特点。

2.1 Kafka的特性
高吞吐量、低延迟：kafka每秒可以处理几十万条消息，它的延迟最低只有几毫秒
可扩展性：kafka集群支持热扩展
持久性、可靠性：消息被持久化到本地磁盘，并且支持数据备份防止数据丢失
容错性：允许集群中节点失败（若副本数量为n,则允许n-1个节点失败）
高并发：支持数千个客户端同时读写


线性回归
