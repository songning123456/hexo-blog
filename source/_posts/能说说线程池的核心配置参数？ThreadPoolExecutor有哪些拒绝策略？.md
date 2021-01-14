---
title: 能说说线程池的核心配置参数？ThreadPoolExecutor有哪些拒绝策略？
date: 2021-01-14 19:43:28
tags: [面试, Java]
category: [面试, Java, 线程]
---

# 核心配置参数？

## corePoolSize(核心线程数)

**默认值1。**

核心线程会一直存在，即使没有任务执行； 
当线程数小于核心线程数的时候，即使有空闲线程，也会一直创建线程直到达到核心线程数；
设置allowCoreThreadTimeout=true(默认false)时，核心线程会超时关闭。

## queueCapacity(任务队列容量)

**默认值Integer.MAX_VALUE。**

也叫阻塞队列，当核心线程都在运行，此时再有任务进来，会进入任务队列，排队等待线程执行。

## maxPoolSize(最大线程数)

**默认值Integer.MAX_VALUE。**

线程池里允许存在的最大线程数量；
当任务队列已满，且线程数量大于等于核心线程数时，会创建新的线程执行任务；
线程池里允许存在的最大线程数量。当任务队列已满，且线程数量大于等于核心线程数时，会创建新的线程执行任务。

## keepAliveTime(线程空闲时间)

**默认值60秒。**

当线程空闲时间达到keepAliveTime时，线程会退出(关闭)，直到线程数等于核心线程数；
如果设置了allowCoreThreadTimeout=true，则线程会退出直到线程数等于零。

## allowCoreThreadTimeout(允许核心线程超时)

**默认值false。**

## rejectedExecutionHandler(任务拒绝处理器)

**默认值AbortPolicy()。**

当线程数量达到最大线程数，且任务队列已满时，会拒绝任务；
调用线程池shutdown()方法后，会等待执行完线程池的任务之后，再shutdown()。如果在调用了shutdown()方法和线程池真正shutdown()之间提交任务，会拒绝新任务。

# 拒绝策略

## AbortPolicy

直接抛异常。

## DiscardPolicy

当前任务会强制调用run先执行，任务将由调用者线程(可能是主线程)去执行。缺点可能会阻塞主线程。

## DiscardOldestPolicy

抛弃任务队列中最旧任务。

## CallerRunsPolicy

抛弃当前将要加入队列的任务。

## 自定义

如果后续慢慢的队列里没任务了，线程空闲了，超过corePoolSize的线程会自动释放掉，在keepAliveTime之后就会释放。