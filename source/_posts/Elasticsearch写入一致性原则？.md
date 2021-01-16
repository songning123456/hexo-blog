---
title: Elasticsearch写入一致性原则？
date: 2021-01-16 09:18:35
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

# consistency

# one(primary shard) 

要求我们这个写操作，只要有一个primary shard是active活跃可用的，就可以执行。

# all(all shard) 

要求我们这个写操作，必须所有的primary shard和replica shard都是活跃的，才可以执行这个写操作。

# quorum(default)

默认的值，要求所有的shard中，必须是大部分的shard都是活跃的，可用的，才可以执行这个写操作quorum=(primary+number_of_replicas)/2+1。

