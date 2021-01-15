---
title: synchronized和Lock的区别？
date: 2021-01-15 11:02:26
tags: [面试, Java]
category: [面试, Java, 并发]
---

# synchronized

关键字，内置语言实现。
在线程发生异常时会自动释放锁，因此不会发生异常死锁。
非中断锁，必须等待线程执行完成释放锁。

# Lock

Lock是接口。
异常时不会自动释放锁，所以需要在finally中实现释放锁。
中断锁。
使用读锁提高多线程读效率。
