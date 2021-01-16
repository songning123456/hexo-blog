---
title: Dubbo为什么需要服务治理？
date: 2021-01-16 12:02:26
tags: [面试, Dubbo]
category: [面试, Dubbo]
---

{% asset_img serviceGovernance.png %}

* 过多的服务URL配置困难；
* 负载均衡分配节点压力过大的情况下也需要部署集群；
* 服务依赖混乱，启动顺序不清晰；
* 过多服务导致性能指标分析难度较大，需要监控。
