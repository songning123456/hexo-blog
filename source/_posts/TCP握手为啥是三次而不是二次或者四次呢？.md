---
title: TCP握手为啥是三次而不是二次或者四次呢？
date: 2021-01-15 13:50:59
tags: [面试, 网络]
category: [面试, 网络]
---

{% asset_img shakehand.png %}

建立三次握手的时候，TCP报头用到了下面几个东西，ACK、SYN、FIN。第一次握手，客户端发送连接请求报文，此时SYN=1、ACK=0，这就是说这是个连接请求，seq=x，接着客户端处于SYN_SENT状态，等待服务器响应。第二次握手，服务端收到SYN=1的请求报文，需要返回一个确认报文，ack=x+1，SYN=1，ACK=1，seq=y，发送给客户端，自己处于SYN_RECV状态。第三次握手，客户端收到了报文，将ack=y+1，ACK=1，seq=x+1。

假设两次握手就ok了。要是客户端第一次握手过去，结果卡在某个地方了，没到服务端；完了客户端再次重试发送了第一次握手过去，服务端收到了，ok了，大家来回来去，三次握手建立了连接。结果，尴尬的是，后来那个卡在哪儿的老的第一次握手发到了服务器，服务器直接就返回一个第二次握手，这个时候服务器开辟了资源准备客户端发送数据啥的，结果呢？客户端根本就不会理睬这个发回去的二次握手，因为之前都通信过了。但是如果是三次握手，那个二次握手发回去，客户端发现根本不对，就会发送个复位的报文过去，让服务器撤销开辟的资源，别等着了。

如果四次挥手的话。第一次挥手，客户端发送报文，FIN=1，seq=u，此时进入FIN-WAIT-1状态。第二次挥手，服务端收到报文，这时候进入CLOSE_WAIT状态，返回一个报文，ACK=1，ack=u+1，seq=v。客户端收到这个报文之后，直接进入FIN-WAIT-2状态，此时客户端到服务端的连接就释放了。第三次挥手，服务端发送连接释放报文，FIN=1，ack=u+1，seq=w，服务端进入LAST-ACK状态。第四次挥手，客户端收到连接释放报文之后，发应答报文，ACK=1，ack=w+1，seq=u+1，进入TIME_WAIT状态，等待一会儿客户端进入CLOSED状态，服务端收到报文之后就进入CLOSED状态。


