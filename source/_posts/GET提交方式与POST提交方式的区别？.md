---
title: GET提交方式与POST提交方式的区别？
date: 2021-01-15 13:25:34
tags: [面试, 网络]
category: [面试, 网络]
---

# GET

* 在浏览器回退时是无害的。
* URL地址可以被收藏。
* 被浏览器主动缓存。
* 只能进行URL编程。
* 请求参数会被完整保留在浏览器历史里。
* 在URL中传送的参数有长度限制，不能大于2KB。
* 只接受ascII字符。
* 参数直接暴露在URL上，所以不能用来传递敏感信息。
* 通过URL传递。
* 不支持文件上传。

# POST

* 再次请求。
* URL地址不会被收藏。
* 不会被浏览器主动缓存，除非手动设置。
* 支持多种编码方式。
* 请求参数不会被保留在浏览器历史里。
* 请求参数没有长度限制。
* 在URL中传送的参数没有长度限制。
* 没有字符限制。
* 传递敏感信息安全。
* 放在request body中。
* 支持文件上传。
