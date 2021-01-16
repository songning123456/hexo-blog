---
title: Nginx实现请求转发的方式？负载均衡的实现方式？
date: 2021-01-16 12:26:08
tags: [面试, 部署]
category: [面试, 部署]
---

**反向代理和负载均衡**

# 轮询(默认)

每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。

```html
upstream backserver { 
    server 192.168.0.14; 
    server 192.168.0.15; 
}
```

# 指定权重

指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。

```html
upstream backserver { 
    server 192.168.0.14 weight=10; 
    server 192.168.0.15 weight=10; 
}  
```

# IP绑定 ip_hash

每个请求按访问ip的hash结果分配，这样每个访客固定访问一个后端服务器，可以解决session的问题。

```html
upstream backserver { 
    ip_hash; 
    server 192.168.0.14:88; 
    server 192.168.0.15:80; 
}
```

# fair(第三方)

按后端服务器的响应时间来分配请求，响应时间短的优先分配。

```html
upstream backserver { 
    server server1; 
    server server2; 
    fair;
}
```

# url_hash(第三方)

按访问url的hash结果来分配请求，使每个url定向到同一个后端服务器，后端服务器为缓存时比较有效。

```html
upstream backserver { 
    server squid1:3128; 
    server squid2:3128;
    hash $request_uri; 
    hash_method crc32; 
}
```


