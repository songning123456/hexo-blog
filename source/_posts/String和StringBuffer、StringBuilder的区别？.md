---
title: String和StringBuffer、StringBuilder的区别？
date: 2021-01-14 14:44:36
tags: [面试, Java]
category: [面试, Java, 基础]
---

# String

String用字符数组保存字符串，private final char value[]，所以String对象是不可变的。也就可以理解为常量，线程安全。每次对String类型进行改变的时候，都会生成一个新的String对象，然后将指针指向新的String对象。

# StringBuffer

StringBuffer继承自AbstractStringBuilder类，在AbstractStringBuilder中也是使用字符数组保存字符串，char[] value，是可变的。对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。本身进行操作，而不是生成新的对象并改变对象引用。 

# StringBuilder

StringBuilder继承自AbstractStringBuilder类，在AbstractStringBuilder中也是使用字符数组保存字符串，char[] value，是可变的。并没有对方法进行加同步锁，所以是非线程安全的。StringBuilder相比使用StringBuffer仅能获得10%~15%左右的性能提升。