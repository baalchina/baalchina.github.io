#下载

`wget https://www.percona.com/downloads/XtraBackup/Percona-XtraBackup-2.4.5/binary/redhat/7/x86_64/Percona-XtraBackup-2.4.5-re41c0be-el7-x86_64-bundle.tar`

#安装
`yum localinstall percona-xtrabackup-24-2.4.5-1.el7.x86_64.rpm`

#全量备份
`xtrabackup --user=username --password=password --backup --target-dir=/data/backups/`
- `--backup`代表备份
- `--target-dir`代表目的地址
- `--prepare`代表准备??，恢复之前必须先`prepare`，否则会有不同步的现象
- `--compress`，如果需要压缩。压缩率还是不错的。

#增量备份
首先做一个全量备份，假设文件在`/data/backup`下
`xtrabackup --backup --target-dir=/data/backups/inc1 --incremental-basedir=/data/backups/`


#恢复
`$ xtrabackup --copy-back --target-dir=/data/backups/ `
- 必须先`prepare`
- 如果不需要备份了，可以用`--move-back`

#一个简单的shell
```
#!/bin/sh

# a backup shell for mysql
# using xtrabackup back mysql to iscsi disk

rm -rf /backup/xtrabackup
xtrabackup --user=root --password=password --backup --compress --target-dir=/backup/xtrabackup
```


