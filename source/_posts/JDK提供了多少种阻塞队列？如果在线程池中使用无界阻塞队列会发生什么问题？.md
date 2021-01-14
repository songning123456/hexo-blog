---
title: JDK提供了多少种阻塞队列？如果在线程池中使用无界阻塞队列会发生什么问题？
date: 2021-01-14 22:12:28
tags: [面试, Java]
category: [面试, Java, 线程]
---

# 阻塞队列

## ArrayBlockingQueue

一个由数组结构组成的有界阻塞队列。

## LinkedBlockingQueue

一个由链表结构组成的有界阻塞队列。

## PriorityBlockingQueue

一个支持优先级排序的无界阻塞队列。

## DelayQueue

一个使用优先级队列实现的无界阻塞队列。

## SynchronousQueue

一个不存储元素的阻塞队列。

## LinkedTransferQueue

一个由链表结构组成的无界阻塞队列。

## LinkedBlockingQueue 

一个由链表结构组成的双向阻塞队列。  

# 线程池

## Executors.newFixedThreadPool(10)

**默认队列LinkedBlockingQueue**

无限加入队列。 

## Executors.newScheduledThreadPool(10)

**默认队列DelayedWorkQueue**

队列如果满了，阻塞。 

## Executors.newSingleThreadScheduledExecutor()

**默认队列DelayedWorkQueue**

队列如果满了，阻塞。 

## Executors.newCachedThreadPool()

**默认队列SynchronousQueue**

队列如果满了，抛异常。 

## Executors.newSingleThreadExecutor()

**默认队列LinkedBlockingQueue**

无限加入队列。 


总结：因为调用异常，会调用超时，线程处理任务时间是超时时间，线程池等待队列，会变得越来越大，此时会导致内存飙升起来，而且还可能导致OOM，内存溢出或者频繁的GC。

