Title: Discuz!的密码加密
Date: 2017-08-25 23:35:53
Tags: discuz,password


- Discuz!的密码在uc的uc_members里，不在cdb_members里
- 加密方式是md5+salt，其中salt是随机数，每个人都不同
- salt保存在uc_members的字段中