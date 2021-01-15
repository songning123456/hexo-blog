---
title: 你知道synchronized的使用场景吗，它是如何使用的？
date: 2021-01-15 10:57:10
tags: [面试, Java]
category: [面试, Java, 并发]
---

# 实例方法

被锁的对象是**类的实例对象**

```java
public synchronized void method() { ... }
```

实例方法，锁住的是该类的实例对象。

# 静态方法

被锁的对象是**类对象**

```java
public static synchronized void method() { ... }
```

静态方法，锁住的是类对象。

# 实例对象

被锁的对象是**类的实例对象**

```java
synchronized(this) { ... }
```

同步代码块，锁住的是该类的实例对象。

# Class对象

被锁的对象是**类对象**

```java
synchronized(Clazz.class) { ... }
```

同步代码块，锁住的是该类的类对象。

# 任意实例对象

被锁的对象是**实例对象Object**

```java
Object object = new Object(); synchronized(object) { ... } 
```

同步代码块，锁住的是配置的实例对象。

