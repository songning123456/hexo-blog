---
title: 你知道Object中定义了哪些方法？
date: 2021-01-14 14:27:35
tags: [面试, Java]
category: [面试, Java, 基础]
---

# public Boolean equals (Object obj)

比较当前对象与obj是否为同一对象。

# public String toString()

返回当前对象的字符串表达形式。

# public native int hashCode()

返回对象的Hash码。Hash码的标志对象的唯一值，Hash码相同的对象是同一对象。

# protected void finalize() throws Throwable

对象销毁时被调用。

# public final native void notify()

唤醒在此对象监视器上等待的单个线程。如果所有线程都在此对象上等待，则会选择唤醒其中一个线程。选择是任意性的，并在对实现做出决定时发生。线程通过调用其中一个wait方法，在对象的监视器上等待。

# public final native void notifyAll()

唤醒在此对象监视器上等待的所有线程。线程通过调用其中一个wait方法，在对象的监视器上等待。

# public final native void wait()

导致调用者线程等待，直到另一个线程调用notify()或者notifyAll()方法，或者指定的等待时间到达。

