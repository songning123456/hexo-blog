---
title: Zookeeper工作原理？
date: 2021-01-16 09:58:36
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

Zookeeper的核心是原子广播，这个机制保证了各个Server之间的同步。实现这个机制的协议叫做Zab协议。Zab协议有两种模式，它们分别是恢复模式(选主)和广播模式(同步)。当服务启动或者在领导者崩溃后，Zab就进入了恢复模式，当领导者被选举出来，且大多数Server完成了和leader的状态同步以后，恢复模式就结束了。状态同步保证了leader和Server具有相同的系统状态。

