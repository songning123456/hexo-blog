---
title: SpringMVC工作原理？
date: 2021-01-15 17:02:34
tags: [面试, SSM]
category: [面试, SSM]
---

{% asset_img SpringMVC.jpeg %}

# 步骤1

客户端发出一个http请求给web服务器，web服务器对http请求进行解析，如果匹配DispatcherServlet的请求映射路径(在web.xml中指定)，web容器将请求转交给DispatcherServlet。

# 步骤2

DispatcherServlet接收到这个请求之后将根据请求的信息(包括URL、Http方法、请求报文头和请求参数Cookie等)以及HandlerMapping的配置找到处理请求的处理器(Handler)。

# 步骤3&&4

DispatcherServlet根据HandlerMapping找到对应的Handler,将处理权交给Handler(Handler将具体的处理进行封装)，再由具体的HandlerAdapter对Handler进行具体的调用。

# 步骤5

Handler对数据处理完成以后将返回一个ModelAndView()对象给DispatcherServlet。

# 步骤6

Handler返回的ModelAndView()只是一个逻辑视图并不是一个正式的视图，DispatcherServlet通过ViewResolver将逻辑视图转化为真正的视图View。

# 步骤7

DispatcherServlet通过model解析出ModelAndView()中的参数进行解析最终展现出完整的view并返回给客户端。
