---
title: Redis实现分布式锁？
date: 2021-01-15 21:23:12
tags: [面试, Redis]
category: [面试, Redis]
---

Redis为单进程单线程模式，采用队列模式将并发访问变成串行访问，且多客户端对Redis的连接并不存在竞争关系Redis中可以使用SETNX命令实现分布式锁。将key的值设为value，当且仅当key不存在。若给定的key已经存在，则SETNX不做任何动作。使用del key命令就能释放锁。

{% asset_img RedisLock.png %}

# 如何解决死锁？

* 通过Redis中expire()给锁设定最大持有时间，如果超过，则Redis来帮我们释放锁；
* 使用setnx key "当前系统时间+锁持有的时间" 和 getset key "当前系统时间+锁持有的时间" 组合的命令就可以实现。


