---
title: Mysql主从复制的原理？
date: 2021-01-15 15:25:10
tags: [面试, 数据库]
category: [面试, 数据库]
---

* master在每个事务更新数据完成之前，将该操作记录串行地写入到binlog文件中。
* slave开启一个I/O Thread，该线程在master打开一个普通连接，主要工作是binlog dump process。如果读取的进度已经跟上了master，就进入睡眠状态并等待master产生新的事件。I/O线程最终的目的是将这些事件写入到中继日志(relay log)中。
* SQL Thread会读取中继日志，并顺序执行该日志中的SQL事件，从而与主数据库中的数据保持一致。

{% asset_img master-slave.png %}
