---
title: Zookeeper是如何保证事务的顺序一致性的？
date: 2021-01-16 09:59:10
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

Zookeeper采用了递增的事务Id来标识，所有的proposal(提议)都在被提出的时候加上了zxid，zxid实际上是一个64位的数字，高32位是epoch(时期、纪元、世、新时代)用来标识leader是否发生改变，如果有新的leader产生出来，epoch会自增，低32位用来递增计数。当新产生proposal的时候，会依据数据库的两阶段过程，首先会向其他的server发出事务执行请求，如果超过半数的机器都能执行并且能够成功，那么就会开始执行。

