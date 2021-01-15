---
title: 能画一张图并解释Spring Boot的核心架构吗？
date: 2021-01-15 17:22:40
tags: [面试, SSM]
category: [面试, SSM]
---

{% asset_img SpringBoot.png %}

# 独立运行Spring项目

Spring Boot可以以jar包形式独立运行，运行一个Spring Boot项目只需要通过java -jar xx.jar来运行。

# 内嵌servlet容器

Spring Boot可以选择内嵌Tomcat、jetty或者Undertow，这样我们无须以war包形式部署项目。

# 提供starter简化Maven配置

Spring提供了一系列的start pom来简化Maven的依赖加载。例如，当你使用了spring-boot-starter-web，会自动加入依赖包。

# 自动装配Spring

SpringBoot会根据在类路径中的jar包，类。为jar包里面的类自动配置Bean，这样会极大地减少我们要使用的配置。当然，SpringBoot只考虑大多数的开发场景，并不是所有的场景，若在实际开发中我们需要配置Bean，而SpringBoot没有提供支持，则可以自定义自动配置。

# 准生产的应用监控

SpringBoot提供基于HTTP SSH Telnet对运行时的项目进行监控。

# 无代码生产和XML配置

Spring Boot不是借助于代码生成来实现的，而是通过条件注解来实现的，这是Spring4.x提供的新特性。
