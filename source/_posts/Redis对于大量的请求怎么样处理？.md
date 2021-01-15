---
title: Redis对于大量的请求怎么样处理？
date: 2021-01-15 21:17:59
tags: [面试, Redis]
category: [面试, Redis]
---

Redis是一个单线程程序，也就说同一时刻它只能处理一个客户端请求。

Redis是通过IO多路复用(select、epoll、kqueue。依据不同的平台，采取不同的实现)来处理多个客户端请求的。

