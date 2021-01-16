---
title: Dubbo有些哪些注册中心？
date: 2021-01-16 11:55:11
tags: [面试, Dubbo]
category: [面试, Dubbo]
---

# Multicast注册中心

Multicast注册中心不需要任何中心节点，只要广播地址，就能进行服务注册和发现。基于网络中组播传输实现。

# Zookeeper注册中心(默认)

基于分布式协调系统Zookeeper实现，采用Zookeeper的watch机制实现数据变更。

# Redis注册中心

基于Redis实现，采用key/Map存储，主key存储服务名和类型，Map中key存储服务URL，value存储服务过期时间。基于redis的发布/订阅模式通知数据变更。

