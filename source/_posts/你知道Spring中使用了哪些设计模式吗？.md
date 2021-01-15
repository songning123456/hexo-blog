---
title: 你知道Spring中使用了哪些设计模式吗？
date: 2021-01-15 15:31:58
tags: [面试, SSM]
category: [面试, SSM]
---

# 单例模式

`<bean scope="singleton"></bean>`
 
# 原型模式

`<bean scope="prototype"></bean>`
 
# 模板模式 

JdbcTemplate 

# 观察者模式 

ApplicationListener 

# 工厂模式-简单工厂模式 

getBean()

# 工厂模式-工厂方法模式 

`<bean factory-method="getInstance"></bean>` 

# 适配器模式  

在AOP实现中的Advice和interceptor之间的转换。

# 装饰者模式

一种是类名中含有Wrapper，另一种是类名中含有Decorator。
  
# 代理模式 

Spring AOP
 
# 策略模式

实例化对象
