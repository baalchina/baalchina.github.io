---
layout:     post
title:      升级Apache+PHP
subtitle:   
date:       2009-10-09 13:26:47
author:     baalchina
header-img:
catalog: true
tags:
  - Apache
  - Linux
  - PHP
---


招生的时候检测报告说俺们的web server有漏洞，于是决定把Apache+PHP升级一下。

首先看一下版本：
```
> [root@www1 ~]# /usr/local/apache2/bin/apachectl -v      
> Server version: Apache/2.2.4 (Unix)       
> Server built:&#160;&#160; Aug&#160; 7 2008 14:07:37  
```

php的版本可以写个phpinfo看到。装的是4.4.4。

```
  > [root@www1 ~]# /usr/local/php/bin/php -i |grep configure      
> Configure Command =&gt;&#160; './configure' '--prefix=/usr/local/php' '--with-apxs2=/usr/local/apache2/bin/apxs' '--with-zlib-dir' '--with-bz2' '--with-tiff-dir' '--with-gd=/usr/local/gd2' '--with-freetype-dir' '--with-jpeg-dir' '--with-png-dir' '--with-ttf' '--enable-mbstring' '--with-mysql=/usr/local/mysql' '--with-config-file-path=/etc' '--disable-ipv6' '--enable-static'
```



更多内容参照：[http://www.baalchina.net/2009/08/php-mysql-apache-configure/](http://www.baalchina.net/2009/08/php-mysql-apache-configure/)

注意：

*   ZO也要装*   根据跑的cms程序，php升级的时候尤其是4~5切记不可太随意。不过php4在07年就停止支持了…*   备份好conf文件，虽然一般不会有问题…
    ###

      > wget [http://cn2.php.net/get/php-5.2.11.tar.gz/from/cn.php.net/mirror](http://cn2.php.net/get/php-5.2.11.tar.gz/from/cn.php.net/mirror)tar xvzf php-5.2.11.tar.gzcd php-5.2.11'./configure' '--prefix=/usr/local/php' '--with-apxs2=/usr/local/apache2/bin/apxs' '--with-zlib-dir' '--with-bz2' '--with-tiff-dir' '--with-gd=/usr/local/gd2' '--with-freetype-dir' '--with-jpeg-dir' '--with-png-dir' '--with-ttf' '--enable-mbstring' '--with-mysql=/usr/local/mysql' '--with-config-file-path=/etc' '--disable-ipv6' '--enable-static'make;make install  

### 然后搞ZO



没啥好说的…bs Zend，居然要注册才给地址

[http://downloads.zend.com/optimizer/3.3.9/ZendOptimizer-3.3.9-linux-glibc23-i386.tar.gz](http://downloads.zend.com/optimizer/3.3.9/ZendOptimizer-3.3.9-linux-glibc23-i386.tar.gz)

另外暂时不支持php5.3.0。



### 然后搞Apache:

&#160;
  > [root@www1 ~]# ./configure &quot;--prefix=/usr/local/apache2&quot; &quot;--enable-module=so&quot; &quot;--enable-deflate=shared&quot; &quot;--enable-expires=shared&quot; &quot;--enable-rewrite=&quot; &quot;--enable-static-support&quot; &quot;--enable-static-htpasswd&quot; &quot;--enable-static-htdigest&quot; &quot;--enable-static-rotatelogs&quot; &quot;--enable-static-logresolve&quot; &quot;--enable-static-htdbm&quot; &quot;--enable-static-ab&quot; &quot;--enable-static-checkgid&quot; &quot;--enable-ssl&quot; &quot;--disable-userdir&quot; &quot;--with-ssl=/usr/local/openssl&quot; &quot;--with-apr=/usr/local/apr&quot; &quot;--with-apr-util=/usr/local/apr-util/bin&quot;      
> [root@www1 ~]# make;make install       
> [root@www1 ~]# /usr/local/apache2/bin/apachectl stop       
> [root@www1 ~]# /usr/local/apache2/bin/apachectl start       
> [root@www1 ~]# /usr/local/apache2/bin/apachectl -v  



打完收工。