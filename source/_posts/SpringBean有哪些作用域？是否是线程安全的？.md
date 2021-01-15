---
title: SpringBean有哪些作用域？是否是线程安全的？
date: 2021-01-15 15:40:17
tags: [面试, SSM]
category: [面试, SSM]
---

# singleton(默认)

线程安全不确定

单例模式，在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例。

# prototype

线程安全

原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例，一般来说下面几种作用域，在开发的时候一般都不会用，99.99%的时候都是用singleton单例作用域。

# request

线程安全不确定

对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。只有在Web应用中使用Spring时，该作用域才有效，在请求完成以后，bean会失效并被垃圾回收器回收。 

# session

线程安全不确定

对于每次HTTP Session，使用session定义的Bean豆浆产生一个新实例。同样只有在Web应用中使用Spring时，该作用域才有效，在session过期后，bean会随之失效。

# globalSession

线程安全不确定

每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。典型情况下，仅在使用portlet context的时候有效。同样只有在Web应用中使用Spring时，该作用域才有效。 


线程安全这个问题，要从单例与原型Bean分别进行说明。对于原型Bean，每次创建一个新对象，也就是线程之间并不存在Bean共享，自然是不会有线程安全的问题。对于单例Bean，所有线程都共享一个单例实例Bean，因此是存在资源的竞争。如果单例Bean，是一个无状态Bean，也就是线程中的操作不会对Bean的成员执行查询以外的操作，那么这个单例Bean是线程安全的。比如SpringMVC的Controller、Service、Dao等，这些Bean大多是无状态的，只关注于方法本身。对于有状态的Bean，Spring官方提供的Bean，一般提供了通过ThreadLocal去解决线程安全的方法，比如RequestContextHolder、TransactionSynchronizationManager、LocaleContextHolder等。
