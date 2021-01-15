---
title: SpringMVC常用的注解？
date: 2021-01-15 17:05:11
tags: [面试, SSM]
category: [面试, SSM]
---

# @Controller

Controller控制器是通过服务接口定义的提供访问应用程序的一种行为，它解释用户的输入，将其转换成一个模型然后将试图呈献给用户。Spring MVC使用@Controller定义控制器，它还允许自动检测定义在类路径下的组件并自动注册。如想自动检测生效，需在XML头文件下引入spring-context。

# @RequestMapping

既可以作用在类级别，也可以作用在方法级别。

# @PathVariable

@PathVariable中的参数可以是任意的简单类型，如int, long, Date等等。Spring会自动将其转换成合适的类型或者抛出TypeMismatchException异常。

# @RequestParam

@RequestParam将请求的参数绑定到方法中的参数上。其实，即使不配置该参数，注解也会默认使用该参数。如果想自定义指定参数的话，如果将@RequestParam的required属性设置为false(如@RequestParam(value="id",required=false))。

# @RequestBody

方法参数应该被绑定到HTTP请求Body上。

# @ResponseBody

将返回类型直接输入到HTTP response body中。

# @RestController

创建REST类型的控制器与@Controller类型。
