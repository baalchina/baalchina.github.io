---
layout:     post
title:      杯具的ipod touch恢复固件
subtitle:   
date:       2010-07-16 19:27:30
author:     baalchina
header-img:
catalog: true
tags:
  - Apple
  - iPod
---

水果的东西实在是太娇贵了，什么时候见过nokia的东西摔了结果摔坏了的？杯具的偶就遇上了…touch莫名奇妙的重力感应失灵，于是打400电话，无解，决定去维修站返修。

为了避免到了维修站出现说我的touch没恢复过让我恢复一次的问题，于是决定自己手工恢复一下。结果遇到了和上次某同学的touch一样的问题…变砖了。

与使用itunes恢复。接上usb，打开itunes，安装power+home 10s之后松开power，itunes提示发现一个出于dfu模式的ipod。恢复。但是网速实在是太慢了…恢复了两天都失败。

想起来电脑上存过一个3.1.3的固件，于是shift+恢复，提示验证失败。很无解，于是google一把。找到这个：

[http://bbs.dospy.com/viewthread.php?fromuid=14292059&amp;tid=6243837&amp;fid=301](http://bbs.dospy.com/viewthread.php?fromuid=14292059&amp;tid=6243837&amp;fid=301 "http://bbs.dospy.com/viewthread.php?fromuid=14292059&amp;tid=6243837&amp;fid=301")

&#160;

原来apple已经关掉了恢复自定义固件的功能。于是用了它2楼的帖子，模拟一个apple服务器。

&#160;

但是又遇到问题了，提示遇到未能恢复，未知错误3002。

仔细看了一下java的命令行，有一些错误，so，重启电脑，再运行，搞定。

&#160;

另外悲剧的是，重力感应依旧失效…过几天去维修站吧…