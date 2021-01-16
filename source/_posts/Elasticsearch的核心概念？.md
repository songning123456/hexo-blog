---
title: Elasticsearch的核心概念？
date: 2021-01-16 09:08:40
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

# Near Realtime(NRT)

近实时，两个意思，从写入数据到数据可以被搜索到有一个小延迟(大概1秒)；基于es执行搜索和分析可以达到秒级。

# Cluster(集群)

包含多个节点，每个节点属于哪个集群是通过一个配置(集群名称，默认是Elasticsearch)来决定的，对于中小型应用来说，刚开始一个集群就一个节点很正常。

# Node(节点)

集群中的一个节点，节点也有一个名称(默认是随机分配的)，节点名称很重要(在执行运维管理操作的时候)，默认节点会去加入一个名称为“Elasticsearch”的集群，如果直接启动一堆节点，那么它们会自动组成一个Elasticsearch集群，当然一个节点也可以组成一个Elasticsearch集群。

# Document(文档)&field

文档，ES中的最小数据单元，一个document可以是一条客户数据，一条商品分类数据，一条订单数据，通常用JSON数据结构表示，每个index下的type中，都可以去存储多个document。一个document里面有多个field，每个field就是一个数据字段。

# Index(索引)

包含一堆有相似结构的文档数据，比如可以有一个客户索引，商品分类索引，订单索引，索引有一个名称。一个index包含很多document，一个index就代表了一类类似的或者相同的document。比如说建立一个product index，商品索引，里面可能就存放了所有的商品数据，所有的商品document。

# Type(类型)

每个索引里都可以有一个或多个type，type是index中的一个逻辑数据分类，一个type下的document，都有相同的field，比如博客系统，有一个索引，可以定义用户数据type，博客数据type，评论数据type。

# shard

单台机器无法存储大量数据，Elasticsearch可以将一个索引中的数据切分为多个shard，分布在多台服务器上存储。有了shard就可以横向扩展，存储更多数据，让搜索和分析等操作分布到多台服务器上去执行，提升吞吐量和性能。每个shard都是一个lucene index。

# replica

任何一个服务器随时可能故障或宕机，此时shard可能就会丢失，因此可以为每个shard创建多个replica副本。replica可以在shard故障时提供备用服务，保证数据不丢失，多个replica还可以提升搜索操作的吞吐量和性能。primary shard(建立索引时一次设置，不能修改，默认5个)，replica shard(随时修改数量，默认1个)，默认每个索引10个shard，5个primary shard，5个replica shard，最小的高可用配置，是2台服务器。
