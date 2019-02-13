Title: 增加特定PHP模块
Date:
URL: 
Tags: 

假设我们要增加`ldap`模块，不需要重新编译。

- 下载完整的php7.2包，解压
- 进入源码包的目录：`php-7.2.8/ext/ldap`
- 运行你机器上现有php的`phpize`文件，假设它在`/www/server/php/72/bin/phpize`
- 编译：`./configure --with-php-config=/www/server/php/72/bin/php-config --with-ldap`
- make
- make install
- 注意编译这里，只要加上`with-ldap`就可以了。很快。
- 修改`php.ini`，重启即可