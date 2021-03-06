首先安装好CentOS 7，这个不多说。

#RPM包的种种
- 当前的GA版本是5.7.17-1，RPM包地址：<https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.17-1.el7.x86_64.rpm-bundle.tar>，略大，557.1M。
- 下载完后可以验证下MD5，#md5sum mysql-standard-5.7.18-linux-i686.tar.gz
- 注意是一个tar包，里面有好多RPM，每个的作用如下：

![](./_image/2017-02-04-23-09-37.jpg)
- 一个标准的MySQL安装需要以下RPM包：`mysql-community-server`, `mysql-community-client`, `mysql-community-libs`, `mysql-community-common`, 以及 `mysql-community-libs-compat` 。
- 所以你需要做的就是解压缩上述tar包，进入该目录，运行`sudo yum install mysql-community-{server,client,common,libs}-* `
- 红帽系（含CentOS和Oracle Linux）还需要运行`shell> sudo yum install mysql-community-{server,client,common,libs}-* mysql-5.* `
- 当然`rpm`命令也可以。`yum`的好处在于可以方便的解决包依赖问题。

#关于
安装的时候遇到了这个错误：
```
Transaction check error:
  file /etc/my.cnf conflicts between attempted installs of mysql-community-server-minimal-5.7.17-1.el7.x86_64 and mysql-community-server-5.7.17-1.el7.x86_64
  file /usr/bin/my_print_defaults conflicts between attempted installs of mysql-community-server-minimal-5.7.17-1.el7.x86_64 and mysql-community-server-5.7.17-1.el7.x86_64

Error Summary
-------------
```
其实还有很多。一开始以为是Mariadb冲突了，删掉之后仍然报这个错误。
后来仔细看了提示，是因为压缩包里有`mysql-community-server-minimal-5.7.17-1.el7.x86_64 `和`mysql-community-server-5.7.17-1.el7.x86_64`两个包，这两个包是冲突的...
这在MySQL安装文档里就有。方法很简单，删掉`mysql-community-server-minimal-5.7.17-1.el7.x86_64`的rpm包就可以了。

#配置文件
装完了之后，你的配置文件在这里：

![](./_image/2017-02-04-23-13-57.jpg)


#管理服务

- 启动服务:`#service mysqld start | stop |status|restart`
- CentOS 7下则是`systemctl {start | stop | status |restart} mysqld` (其实service也可以..)
- systemd还有更强大的功能，例如配置多实例，配置其他命令，详见<https://dev.mysql.com/doc/refman/5.7/en/using-systemd.html>

#密码
- 默认mysql会在`/var/log/mysqld.log`下建立随机的root密码
- 进去改一下密码就好了`mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';`
- 允许远程访问
```
mysql>grant all privileges on *.* to 'root'@'%' identified by 'MyNewPass4!' with grant option;  
mysql> flush privileges;
```


#防火墙
对于CentOS7，还需要打开防火墙，
```
firewall-cmd --add-service=mysql --permanent 
firewall-cmd --reload
```

#然后
然后，就没有然后啦！Enjoy Mysql!


#参考：
- Installing MySQL on Linux Using RPM Packages from Oracle: <https://dev.mysql.com/doc/refman/5.7/en/linux-installation.html>