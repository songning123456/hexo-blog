---
title: Elasticsearch document路由原理？
date: 2021-01-16 09:17:45
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

* 当客户端创建document的时候，ES就需要决定这个doc是放在这个index的哪个shard上，这个过程称为document routing，即数据路由。
* primary shard一旦index建立，是不允许修改的，但是replica shard可以随时修改。
* 路由算法：shard = hash(routing) % number_of_primary_shards。
* 从hash函数中，产出的hash值一定是相同的。
* 无论hash值是几，无论是什么数字，对number_of_primary_shards求余数，结果一定是在0~number_of_primary_shards-1之间这个范围内的。
