Title: Oracle ODI学习笔记3 字符集问题
一个MS Sql到Oracle的转换，源数据都是`char`类型，目标是`vchar2`类型。
- 目标字段要远大于源字段
- 如果发现中间表超出，类似这个提示：
```
ODI-1228: 任务Load data-LKM SQL to Oracle-在目标连接orcl上失败。
Caused By: java.sql.BatchUpdateException: ORA-12899: 列 "USR"."C$_0SY_JBGR"."BJHM" 的值太大 (实际值: 54, 最大值: 50)
```
- 解决办法是修改`源模型`，将这个字段调大即可。