---
title: '@SpringBootApplication包含哪些注解？'
date: 2021-01-15 17:28:34
tags: [面试, SSM]
category: [面试, SSM]
---

# @ComponentScan

扫描当前包及其子包下被@Component，@Controller，@Service，@Repository注解标记的类并纳入到Spring容器进行管理。

# @SpringBootConfiguration

继承自@Configuration，二者功能一致，标注当前类是配置类，并会将当前类内声明的一个或多个以@Bean注解标记的方法的实例纳入到Spring容器中，并且实例名就是方法名。

# @EnableAutoConfiguration

启动自动的配置，@EnableAutoConfiguration注解的意思就是SpringBoot根据你添加的jar包来配置你项目的默认配置。

