---
title: Zookeeper watch机制？
date: 2021-01-16 10:03:14
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

* 一次性触发数据发生改变时，一个watcher event会被发送到client，但是client只会收到一次这样的信息。
* watcher event异步发送watcher的通知事件从server发送到client是异步的，这就存在一个问题，不同的客户端和服务器之间通过socket进行通信，由于网络延迟或其他因素导致客户端在不通的时刻监听到事件，由于Zookeeper本身提供了ordering guarantee，即客户端监听事件后，才会感知它所监视znode发生了变化。所以我们使用Zookeeper不能期望能够监控到节点每次的变化。Zookeeper只能保证最终的一致性，而无法保证强一致性。
* 数据监视Zookeeper有数据监视和子数据监视get data() and exists()设置数据监视，get children()设置了子节点监视。
* 注册watcher getData、exists、getChildren。
* 触发watcher create、delete、setData。
* setData()会触发znode上设置的data watch(如果set成功的话)。一个成功的create()操作会触发被创建的znode上的数据watch，以及其父节点上的child watch。而一个成功的delete()操作将会同时触发一个znode的data watch和child watch(因为这样就没有子节点了)，同时也会触发其父节点的child watch。
* 当一个客户端连接到一个新的服务器上时，watch将会被以任意会话事件触发。当与一个服务器失去连接的时候，是无法接收到watch的。而当client重新连接时，如果需要的话，所有先前注册过的watch，都会被重新注册。通常这是完全透明的。只有在一个特殊情况下，watch可能会丢失：对于一个未创建的znode的exist watch，如果在客户端断开连接期间被创建了，并且随后在客户端连接上之前又删除了，这种情况下，这个watch事件可能会被丢失。
* Watch是轻量级的，其实就是本地JVM的Callback，服务器端只是存了是否有设置了Watcher的布尔类型。

