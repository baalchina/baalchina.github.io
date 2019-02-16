---
layout:     post
title:      查看MySQL，Apache，PHP的编译参数
subtitle:   
date:       2009-08-02 10:36:54
author:     baalchina
header-img:
catalog: true
tags:
  - Apache
  - PHP
  - Mysql
  - Linux
---



# 查看mysql编译参数：
  > cat /usr/local/mysql/bin/mysqlbug | grep CONFIGURE_LINE  

# 查看apache编译参数：
  > cat $apachehome$/build/config.nice  

也可以用
  > httpd –l  

或者
  > httpd -v  

# 查看php编译参数：
  > $PHP$/bin/php -i | grep configure  


当然，写个phpinfo也是可以的。
  > <?php phpinfo();?>;