---
title: 你知道JVM是如何运行起来的吗？我们的对象是如何分配的？
date: 2021-01-15 11:30:49
tags: [面试, Java]
category: [面试, Java, 虚拟机]
---

有一个类里面包含了一个main方法，你去执行这个main方法，此时会启动一个jvm进程，他会默认就会有一个main线程，这个main线程就负责执行这个main方法的代码，进而创建各种对象。一般tomcat，类都会加载到jvm里去，spring容器而言都会对我们的类进行实例化成bean，有工作线程会来执行我们的bean实例对象里的方法和代码，进而也会创建其他的各种对象，实现业务逻辑。


{% asset_img JVMRun.png %}
