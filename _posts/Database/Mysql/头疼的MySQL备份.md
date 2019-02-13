服务器年前差点挂了，于是想着还是做个备份，虽然VMWare每天一备，但毕竟快照总有不靠谱的时候。

查了下，`Netbackup`居然不支持MySQL，需要购买商业插件。
然后MySQL倒是有一个很牛逼的备份软件`Percona XtraBackup`，还是开源免费的：https://www.percona.com/doc/percona-xtrabackup/2.4/installation/yum_repo.html。
不过这老兄只支持CentOS5以上，结果一看我的服务器，是CentOS 4.4的，也难怪，这机器跑了10年了...

慢慢折腾吧...