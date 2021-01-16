---
title: Dubbo的整体架构设计有哪些分层？
date: 2021-01-16 12:00:11
tags: [面试, Dubbo]
category: [面试, Dubbo]
---

# 服务接口层(Service)

该层与业务逻辑相关，根据provider和consumer的业务设计对应的接口和实现。

# 配置层(Config)

对外配置接口，以ServiceConfig和ReferenceConfig为中心。

# 服务代理层(Proxy)

服务接口透明代理，生成服务的客户端Stub和服务器端Skeleton。

# 服务注册层(Registry)

封装服务地址的注册与发现，以服务URL为中心。

# 路由层(Cluster)

封装多个提供者的路由和负载均衡，并桥接注册中心，以Invoker为中心，扩展接口为Cluster、Directory、Router和LoadBalance。

# 集群层(Cluster)

封装多个提供者的路由及负载均衡，并桥接注册中心，以Invoker为中心。

# 监控层(Monitor)

RPC调用次数和调用时间监控。

# 远程调用层(Protocol)

封装RPC调用，以Invocation和Result为中心，扩展接口为Protocol、Invoker和Exporter。

# 信息交换层(Exchange)

封装请求响应模式，同步转异步，以Request和Response为中心。

# 网络传输层(Transport)

抽象mina和netty为统一接口，以Message 为中心。

