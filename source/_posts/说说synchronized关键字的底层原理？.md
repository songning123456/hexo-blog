---
title: 说说synchronized关键字的底层原理？
date: 2021-01-15 10:56:19
tags: [面试, Java]
category: [面试, Java, 并发]
---

synchronized同步语句块的实现，使用的是**monitorenter**和**monitorexit**指令，其中monitorenter指令指向同步代码块的开始位置，monitorexit指令则指明同步代码块的结束位置。 当执行monitorenter指令时，线程试图获取锁，也就是获取monitor(monitor对象存在于每个Java对象的对象头中，synchronized锁便是通过这种方式获取锁的，这也是为什么Java中任意对象都可以作为锁的原因)的持有权。当计数器为0，则可以成功获取，获取后将锁计数器设为1，也就是加1；相应的，在执行monitorexit指令后，将锁计数器设为0，表明锁被释放。如果获取对象锁失败，那当前线程就要阻塞等待，直到锁被另外一个线程释放为止。
