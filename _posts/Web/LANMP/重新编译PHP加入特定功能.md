重新编译了一下php，增加ftp功能

编译代码
```
#./configure --prefix=/usr/local/php --with-config-file-path=/etc --with-mysql=/usr/local/mysql --with-mysqli=/usr/local/mysql/bin/mysql_config --with-iconv-dir=/usr/local --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir=/usr --enable-xml --enable-safe-mode --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --with-curlwrappers --enable-mbregex --enable-fpm --enable-mbstring --with-mcrypt --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc --enable-zip --enable-soap --enable-ftp
#make ZEND_EXTRA_LIBS='-liconv'
#make install
```
注意直接`make`不行，会报libicon错误

安装完，用`/usr/local/php/sbin/php-fpm -m`看看模块是否正常。

然后重启php-fpm和nginx即可