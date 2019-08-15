---
layout:     post
title:      nginx反向代理支持WebSocket
subtitle:   
date:       2019-08-15
author:     baalchina
header-img:
catalog: true
tags:
  - WebSocket
  - nginx
---


> WebSocket 协议提供了一种创建支持客户端和服务端实时双向通信Web应用程序的方法。作为HTML5规范的一部分，WebSockets简化了开发Web实时通信程序的难度。目前主流的浏览器都支持WebSockets，包括火狐、IE、Chrome、Safari以及Opera等，而且，越来越多的服务器应用框架也开始支持WebSockets。

>要在企业产品中使用WebSockets，为满足高性能和高可用性，需要多个WebSocket服务器。负载均衡层需要支持WebSocket协议。Nginx从1.3版起就开始支持WebSocket协议，而且可以担当WebSocket应用程序的反向代理以及实现负载均衡。

>WebSocket协议和HTTP协议不同，但是WebSocket协议的握手和HTTP是兼容的，它使用HTTP的Upgrade协议头将连接从HTTP连接升级到WebSocket连接。这个特性使得WebSocket应用程序可以很容易地应用到现有的基础设施。例如，WebSocket应用可以使用标准的80和443 HTTP端口，因此可以通过现有的防火墙设施。

>WebSockets应用程序会在客户端和服务器之间建立一个长连接，使得开发实时应用很容易。HTTP的Upgrade协议头机制用于将连接从HTTP连接升级到WebSocket连接，Upgrade机制使用了Upgrade协议头和Connection协议头。反向代理服务器在支持WebSocket协议方面面临着一些挑战。挑战之一是WebSocket是一个逐段转发（hop-by-hop）协议，因此当代理服务器拦截到来自客户端的Upgrade请求时，代理服务器需要将自己的Upgrade请求发送给后端服务器，包括适合的请求头。而且，由于WebSocket连接是长连接，与传统的HTTP端连接截然不同，故反向代理服务器还需要允许这些连接处于打开（Open）状态，而不能因为其空闲就关闭了连接。

>Nginx通过在客户端和后端服务器之间建立隧道来支持WebSockets通信。为了让Nginx可以将来自客户端的Upgrade请求发送到后端服务器，Upgrade和Connection的头信息必须被显式的设置。如下所示：


```

location /wsapp/ {
    proxy_pass http://wsbackend;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
```