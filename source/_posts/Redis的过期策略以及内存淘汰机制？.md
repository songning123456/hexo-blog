---
title: Redis的过期策略以及内存淘汰机制？
date: 2021-01-15 21:11:31
tags: [面试, Redis]
category: [面试, Redis]
---

Redis采用的是**定期删除**+**惰性删除**策略。

# 为什么不用定时删除策略？

定时删除，用一个定时器来负责监视key，过期则自动删除。虽然内存及时释放，但是十分消耗CPU资源。在大并发请求下，CPU要将时间应用在处理请求，而不是删除key，因此没有采用这一策略。


# 定期删除+惰性删除是如何工作的呢？

定期删除，Redis默认每个100ms检查，是否有过期的key，有过期key则删除。需要说明的是，Redis不是每个100ms将所有的key检查一次，而是随机抽取进行检查(如果每隔100ms，全部key进行检查，Redis岂不是卡死)。因此，如果只采用定期删除策略，会导致很多key到时间没有删除。于是，惰性删除派上用场。也就是说在你获取某个key的时候，Redis会检查一下，这个key如果设置了过期时间那么是否过期了？如果过期了此时就会删除。


# 采用定期删除+惰性删除就没其他问题了么？

不是的，如果定期删除没删除key。然后你也没即时去请求key，也就是说惰性删除也没生效。这样，Redis的内存会越来越高。那么就应该采用内存淘汰机制。在redis.conf中有一行配置。

```html
maxmemory-policy volatile-lru
```


| <div style="width: 190px">maxmemory-policy参数</div> | 解释 |
| :----- | :----- |
| <div style="width: 190px;font-weight: bold;color:red;">volatile-lru(默认)</div> | 从已设置过期时间的数据集(server.db[i].expires)中挑选最近最少使用的数据淘汰。 |
| <div style="width: 190px;font-weight: bold;">volatile-ttl</div> | 从已设置过期时间的数据集(server.db[i].expires)中挑选将要过期的数据淘汰。 |
| <div style="width: 190px;font-weight: bold;">volatile-random</div> | 从已设置过期时间的数据集(server.db[i].expires)中任意选择数据淘汰。 |
| <div style="width: 190px;font-weight: bold;">allkeys-lru</div> | 从数据集(server.db[i].dict)中挑选最近最少使用的数据淘汰。 |
| <div style="width: 190px;font-weight: bold;">allkeys-random</div> | 从数据集(server.db[i].dict)中任意选择数据淘汰。 |
| <div style="width: 190px;font-weight: bold;">no-enviction</div> | 禁止驱逐数据，新写入操作会报错。 |


如果没有设置expire的key，不满足先决条件(prerequisites)；那么volatile-lru，volatile-random和volatile-ttl策略的行为和noeviction(不删除)基本上一致。


