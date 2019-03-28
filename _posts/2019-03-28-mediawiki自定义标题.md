---
layout:     post
title:      mediawiki自定义标题
subtitle:   
date:       2019-03-28
author:     baalchina
header-img:
catalog: true
tags:
  - wiki
  - mediawiki
---

在mediawiki里，url是`https://net.nau.edu.cn/index.php/VM`，标题那就是`VM`，如果要显示虚拟机

```
$wgAllowDisplayTitle，设置为True
$wgRestrictDisplayTitle = false;
```

前者是允许自定义标题，后者是允许
因为默认只允许大小写，比如IPod修改为iPod

ref
https://www.mediawiki.org/wiki/Help:Magic_words/zh
https://www.mediawiki.org/wiki/Manual:$wgAllowDisplayTitle/zh