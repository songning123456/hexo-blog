---
title: Redis常见性能问题和解决方案？
date: 2021-01-15 21:19:06
tags: [面试, Redis]
category: [面试, Redis]
---

* Master最好不要做任何持久化工作，如RDB内存快照和AOF日志文件；
* 如果数据比较重要，某个Slave开启AOF备份数据，策略设置为每秒同步一次；
* 为了主从复制的速度和连接的稳定性，Master和Slave最好在同一个局域网内；
* 尽量避免在压力很大的主库上增加从库；
* 主从复制不要用图状结构，用单向链表结构更为稳定，即：Master <- Slave1 <- Slave2 <- Slave3 ......

