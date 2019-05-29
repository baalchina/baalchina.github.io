---
layout:     post
title:      vmware导入中文ovf文件
subtitle:   
date:       2019-05-29
author:     baalchina
header-img:
catalog: true
tags:
  - vmware
  - ovf
---


某虚拟机，中文命名，从`vsphere client`里导出的ovf文件也是中文的，分别是4个文件：
- a.mf
- a.ovf
- a.disk1.vmdk
- a.disk2.vmdk


因为vc是6.7了，所以只能用webclient，导入的时候，先是报找不到`vmdk`文件，怀疑是中文问题，于是改名为全英文。

注意还需要修改`.mf`和`.ovf`文件。ovf中要把所有中文改为英文，mf其实是SHA`值，需要在修改完ovf之后重新校验。

另外校验也很简单,windows自带了。

```certutil -hashfile 172-101-1-disk1.vmdk SHA1``` 这样就行。


然后再导入就ok了