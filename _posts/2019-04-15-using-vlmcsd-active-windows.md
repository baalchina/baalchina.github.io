---
layout:     post
title:      使用vlmcsd激活Windows
subtitle:   
date:       2019-04-15
author:     baalchina
header-img:
catalog: true
tags:
  - vlmcsd
---


Windows 10 企业版 + Office 2019，可以用`vlmcsd`激活。

新建一台虚拟机，配置如下：
- 16m内存
- 1cpu
- 不要硬盘
- 软盘
- 网卡

挂载`floppy144.vfd`，启动即可。启动之后可以看到ip。

然后cmd里面运行激活命令即可搞定。


之前在`windows`下运行`vlmcsd`死活报`0x8007000D`，查了下，说是网络问题？

用vmware很轻松解决了。