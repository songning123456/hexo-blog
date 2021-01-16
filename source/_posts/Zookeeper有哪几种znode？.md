---
title: Zookeeper有哪几种znode？
date: 2021-01-16 09:45:04
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

# PERSISTENT-持久化目录节点

客户端与Zookeeper断开连接后，该节点依旧存在。

# PERSISTENT_SEQUENTIAL-持久化顺序编号目录节点

客户端与Zookeeper断开连接后，该节点依旧存在，只是Zookeeper给该节点名称进行顺序编号。

# EPHEMERAL-临时目录节点

客户端与Zookeeper断开连接后，该节点被删除。

# EPHEMERAL_SEQUENTIAL-临时顺序编号目录节点

客户端与Zookeeper断开连接后，该节点被删除，只是Zookeeper给该节点名称进行顺序编号。

