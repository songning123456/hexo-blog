---
title: Zookeeper是如何选取主leader的？
date: 2021-01-16 10:01:30
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

当leader崩溃或者leader失去大多数的follower，这时Zookeeper进入恢复模式，恢复模式需要重新选举出一个新的leader，让所有的Server都恢复到一个正确的状态。Zookeeper的选举算法有两种：一种是基于basic paxos实现的，另外一种是基于fast paxos算法实现的。系统默认的选举算法为fast paxos。

