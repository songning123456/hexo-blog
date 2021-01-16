---
title: 磁盘文件如何合并(segment merge)？
date: 2021-01-16 09:35:07
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

每秒一个segment file文件过多，而且每次search都要搜索所有的segment，很耗时。默认会在后台执行segment merge操作。在merge的时候，被标记为deleted的document也会被彻底物理删除。

每次merge操作的执行流程：

1. 选择一些有相似大小的segment，merge成一个大的segment；
2. 将新的segment flush到磁盘上去；
3. 写一个新的commit point，包括了新的segment，并且排除旧的那些segment；
4. 将新的segment打开供搜索；
5. 将旧的segment删除。
