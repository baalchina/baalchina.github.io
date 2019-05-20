---
layout:     post
title:      DNS的zone文件
subtitle:   
date:       2019-05-18
author:     baalchina
header-img:
catalog: true
tags:
  - dns
  - bind
---

在`bind`里新建了一个`zone`,解析异常，发现日志里很多错误：

```
May 18 19:39:51 dns1 named[5756]: lab.nau.host:41: ignoring out-of-zone data (dc1)
May 18 19:39:51 dns1 named[5756]: lab.nau.host:42: ignoring out-of-zone data (doc)
May 18 19:39:51 dns1 named[5756]: lab.nau.host:43: ignoring out-of-zone data (door)
May 18 19:39:51 dns1 named[5756]: lab.nau.host:44: ignoring out-of-zone data (dzsw)
May 18 19:39:51 dns1 named[5756]: lab.nau.host:45: ignoring out-of-zone data (dzzw)
May 18 19:39:51 dns1 named[5756]: lab.nau.host:46: ignoring out-of-zone data (e10)
```

查了下，发现zone文件里写错了

原来把`$ORIGIN .`写在了最前面，注释掉掉ok了。当没有`$ORIGIN`的时候，默认下面的记录就会以`named.conf`里的zone作为结尾。