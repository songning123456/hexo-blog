---
title: shard&&replica机制？
date: 2021-01-16 09:13:48
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

* index包含多个shard；
* 每个shard都是一个最小工作单元，承载部分数据，lucene实例，完整的建立索引和处理请求的能力；
* 增减节点时，shard会自动在nodes中负载均衡；
* primary shard和replica shard，每个document肯定只存在于某一个primary shard以及其对应的replica shard中，不可能存在于多个primary shard；
* replica shard是primary shard的副本，负责容错，以及承担读请求负载；
* primary shard的数量在创建索引的时候就固定了，replica shard的数量可以随时修改；
* primary shard的默认数量是5，replica默认是1，默认有10个shard，5个primary shard，5个replica shard；
* primary shard不能和自己的replica shard放在同一个节点上(否则节点宕机，primary shard和副本都丢失，起不到容错的作用)，但是可以和其他primary shard的replica shard放在同一个节点上。

