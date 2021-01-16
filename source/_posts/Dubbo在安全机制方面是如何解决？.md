---
title: Dubbo在安全机制方面是如何解决？
date: 2021-01-16 12:09:05
tags: [面试, Dubbo]
category: [面试, Dubbo]
---

Dubbo通过Token令牌防止用户绕过注册中心直连，然后在注册中心上管理授权。Dubbo还提供服务黑白名单，来控制服务所允许的调用方。

