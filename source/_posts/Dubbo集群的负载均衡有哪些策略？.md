---
title: Dubbo集群的负载均衡有哪些策略？
date: 2021-01-16 11:58:43
tags: [面试, Dubbo]
category: [面试, Dubbo]
---

# Random LoadBalance

随机选取提供者策略，有利于动态调整提供者权重。截面碰撞率高，调用次数越多，分布越均匀。

# RoundRobin LoadBalance

轮循选取提供者策略，平均分布，但是存在请求累积的问题。

# LeastActive LoadBalance

最少活跃调用策略，解决慢提供者接收更少的请求。

# ConstantHash LoadBalance

一致性Hash策略，使相同参数请求总是发到同一提供者，一台机器宕机，可以基于虚拟节点，分摊至其他提供者，避免引起提供者的剧烈变动。


