Title: ODI学习笔记7 增量更新之一
Date:
URL: 
Tags: 

测试了下ODI的增量更新（Incremental Update)。环境如下：
- 源表和目标都是Oracle 11gR2
- 源表数据 ：30659098条，目标表数据：30635537条
- IKM用的就是IKM Oracle Incremental Update，所有选项默认（不truncate目标表 )

结果如下：
- 整个会话用了`58分18秒`...
- 最长的两个步骤分别如下：
- 第一个是 `Load Data- LKM SQL to Oracle`，即从源表将所有数据插入到目标库的`C$_OM_XXX`表中。花了`35:57`秒，毕竟3000多万条数据...
- 第二个是`Insert flow into I$ table - IKM Oracle Incremental Update`,看内容是将差一的`23561`条数据插入到目标库的`I$_XXX`表，花了`19分45秒`。
- 然后其他步骤就非常快了。

所以，结论
- 这种表不能用默认的增量更新啊。。。还是起CDC吧...
- 确认两边数据一致的情况下，第二次运行，`Load data`还是很慢，现在已经13分钟了，还没完。。。
明天研究了CDC再来发~
