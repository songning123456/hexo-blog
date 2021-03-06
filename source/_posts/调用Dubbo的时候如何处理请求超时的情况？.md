---
title: 调用Dubbo的时候如何处理请求超时的情况？
date: 2021-01-16 11:05:10
tags: [面试, Dubbo]
category: [面试, Dubbo]
---

Dubbo在调用服务不成功时，默认是会重试两次的。这样在服务端的处理时间超过了设定的超时时间时，就会有重复请求，比如在发邮件时，可能就会发出多份重复邮件，执行注册请求时，就会插入多条重复的注册数据，那么怎么解决超时问题呢？

<span style="color: red">对于核心的服务中心，去除Dubbo超时重试机制，并重新评估设置超时时间。</span>

<span style="color: red">业务处理代码必须放在服务端，客户端只做参数验证和服务调用，不涉及业务流程处理。</span>

```
<!-- 延迟到Spring初始化完成后，再暴露服务,服务调用超时设置为6秒,超时不重试-->  
<dubbo:provider delay="-1" timeout="6000" retries="0"/>
```

当然Dubbo的重试机制其实是非常好的QOS保证，它的路由机制，是会帮你把超时的请求路由到其他机器上，而不是本机尝试，所以dubbo的重试机器也能一定程度的保证服务的质量。但是请一定要综合线上的访问情况，给出综合的评估。

