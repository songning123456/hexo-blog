---
title: Zookeeper下Server工作状态？
date: 2021-01-16 10:00:08
tags: [面试, ZooKeeper]
category: [面试, ZooKeeper]
---

每个Server在工作过程中有三种状态：

# LOOKING

当前Server不知道leader是谁，正在搜寻。

# LEADING

当前Server即为选举出来的leader。

# FOLLOWING

leader已经选举出来，当前Server与之同步。 


