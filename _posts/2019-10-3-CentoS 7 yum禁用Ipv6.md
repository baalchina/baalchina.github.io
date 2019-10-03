---
layout:     post
title:      Cent OS 7 yum 禁用ipv6
subtitle:   
date:       2010-08-06 10:45:42
author:     baalchina
header-img:
catalog: true
tags:
  - CentOS
---


# 修改yum配置文件
vi /etc/yum.conf
# 增加ip解析配置
ip_resolve=4
# 更新确认
yum update