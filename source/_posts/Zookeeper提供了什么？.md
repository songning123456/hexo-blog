---
title: Zookeeper提供了什么？
date: 2021-01-16 09:43:48
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

# 文件系统

Zookeeper提供一个多层级的节点命名空间(节点称为znode)。与文件系统不同的是，这些节点都可以设置关联的数据，而文件系统中只有文件节点可以存放数据而目录节点不行。Zookeeper为了保证高吞吐和低延迟，在内存中维护了这个树状的目录结构，这种特性使得Zookeeper不能用于存放大量的数据，每个节点的存放数据上限为1M。

# 通知机制

client端会对某个znode建立一个watcher事件，当该znode发生变化时，这些client会收到Zookeeper的通知，然后client可以根据znode变化来做出业务上的改变等。
