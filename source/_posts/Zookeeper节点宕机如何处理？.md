---
title: Zookeeper节点宕机如何处理？
date: 2021-01-16 10:02:36
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

Zookeeper本身也是集群，推荐配置不少于3个服务器。Zookeeper自身也要保证当一个节点宕机时，其他节点会继续提供服务。如果是一个Follower宕机，还有2台服务器提供访问，因为Zookeeper上的数据是有多个副本的，数据并不会丢失;如果是一个Leader宕机，Zookeeper会选举出新的Leader。

Zookeeper集群的机制是只要超过半数的节点正常，集群就能正常提供服务。只有在Zookeeper节点挂得太多，只剩一半或不到一半节点能工作，集群才失效。所以3个节点的cluster可以挂掉1个节点(leader可以得到2票>1.5)，2个节点的cluster就不能挂掉任何1个节点了(leader可以得到1票<=1)。
