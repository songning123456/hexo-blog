---
title: 你知道DNS域名解析的流程吗？
date: 2021-01-15 13:37:27
tags: [面试, 网络]
category: [面试, 网络]
---

{% asset_img DNS.png %}
* 浏览器先检查自身缓存中有没有被解析过的这个域名对应的IP地址。如果有，解析结束，同时域名被缓存的时间也可通过TTL属性来设置。
* 如果浏览器缓存中没有，浏览器会检查操作系统缓存中有没有对应的已解析过的结果。而操作系统也有一个域名解析的过程。在windows中可通过C盘里一个叫hosts的文件来设置，如果你在这里指定了一个域名对应的IP地址，那浏览器会首先使用这个IP地址。但是这种操作系统级别的域名解析规程也被很多黑客利用，通过修改你的hosts文件里的内容把特定的域名解析到他指定的IP地址上，造成所谓的域名劫持。所以在windows7中将hosts文件设置成了readonly，防止被恶意篡改。
{% asset_img hosts.PNG %}
* 如果至此还没有命中域名，才会真正的请求本地域名服务器(LDNS)来解析这个域名，这台服务器一般在你的城市的某个角落，距离你不会很远，并且这台服务器的性能都很好，一般都会缓存域名解析结果，大约80%的域名解析到这里就完成了。
* 如果LDNS仍然没有命中，就直接跳到Root Server域名服务器请求解析。
* 根域名服务器返回给LDNS一个所查询域的主域名服务器(gTLD Server，国际顶尖域名服务器，如.com .cn .org等)地址。
* 此时LDNS再发送请求给上一步返回的gTLD。
* 接受请求的gTLD查找并返回这个域名对应的Name Server的地址，这个Name Server就是网站注册的域名服务器。
* Name Server根据映射关系表找到目标IP，返回给LDNS。
* LDNS缓存这个域名和对应的IP。
* LDNS把解析的结果返回给用户，用户根据TTL值缓存到本地系统缓存中，域名解析过程至此结束。

