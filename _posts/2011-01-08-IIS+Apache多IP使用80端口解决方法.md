Title: IIS+Apache多IP，使用80端口解决方法
Date: 2011-01-08 14:29:59
URL: /2011/01/apache-iis-ip-address/
Tags: Apache , iis

Windows 2003，IIS+Apache，两个IP，分别绑定IIS/Apache，但是只能启动一个，状况就是类似于80被占用。

&#160;

解决方法：

Win2003CD找到support/tools/Support.cab，找到httpdcf.exe。然后运行：

&#160;
  > httpcfg set iplisten –i 192.168.1.1  

即将IIS绑到192.168.1.1的80端口。
  > httpcfg query iplisten  

可以查看绑定状况。但是必须先运行前者。

Apache不需要特别设置，直接绑定即可。

&#160;

另外，切忌重启服务器。否则还是不生效。

不知道微软为啥搞这么复杂。