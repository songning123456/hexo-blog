---
title: ES的写入流程(buffer、segment、commit)？
date: 2021-01-16 09:32:13
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

* 数据写入buffer缓冲和translog日志文件；
* 每隔一秒钟，buffer中的数据被写入新的segment file，并进入os cache，此时segment被打开并供search使用，不立即执行commit。(数据写入os cache，并被打开供搜索的过程，叫做refresh，默认是每隔1秒refresh一次。也就是说，每隔一秒就会将buffer中的数据写入一个新的index segment file，先写入os cache中。所以，ES是近实时的，数据写入到可以被搜索，默认是1秒。)
* buffer被清空；
* 重复1~3，新的segment不断添加，buffer不断被清空，而translog中的数据不断累加；
* 当translog长度达到一定程度的时候，commit操作发生。
  1.buffer中的所有数据写入一个新的segment，并写入os cache，打开供使用；
  2.buffer被清空；
  3.一个commit point被写入磁盘，标明了所有的index segment；
  4.filesystem cache中的所有index segment file缓存数据，被fsync强行刷到磁盘上；
  5.现有的translog被清空，创建一个新的translog。
    