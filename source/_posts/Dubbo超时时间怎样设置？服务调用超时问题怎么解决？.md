---
title: Dubbo超时时间怎样设置？服务调用超时问题怎么解决？
date: 2021-01-16 11:03:44
tags: [面试, Dubbo]
category: [面试, Dubbo]
---

# 服务提供者端设置超时时间

在Dubbo的用户文档中，推荐如果能在服务端多配置就尽量多配置，因为服务提供者比消费者更清楚自己提供的服务特性。

# 服务消费者端设置超时时间

如果在消费者端设置了超时时间，以消费者端为主，即优先级更高。因为服务调用方设置超时时间控制性更灵活。如果消费方超时，服务端线程不会定制，会产生警告。


**Dubbo在调用服务不成功时，默认是会重试两次的。**