Oracle ODI学习笔记（1）

#0.备注
- 如果没有特殊说明，版本均是12C，也就是`12.2.1.3.0`
- 个人测试结果，并不保证准确。
- OS：Windows Server 2016,
- DB：Oracle 12c R2
- Update：20180222

#1.概述
- ODI的Agent是用来调度任务的，所以如果你需要任务定期执行，则必须通过Agent（也就是代理）来完成。
- Agent通过`Weblogic`来管理，如果需要配置Agent，需要启动`config.cmd`，我的在这里`C:\Oracle\Middleware\Oracle_Home\oracle_common\common\bin`，运行之后就会启动`Fusion Middleware 配置向导`，很简单，都是中文的
#2.开始配置
- 开始配置，选择一个空目录
- 模板部分，记得选择`Oracle Data Intergrator-Standalone Agent`
- 下面都不复杂，需要注意的是，在`数据库配置类型`这一步，方案所有者应当是默认的`DEV_STB`，而不是ODI的账号`DEV_ODI_REPO`，口令是ODI的口令
- 下面可以添加Agent的名字，一次可以多个，注意**区分大小写**
- 然后一路NEXT，提交即可
- 记得要在ODI里面添加这个Agent，否则无法启动

#3.启动Agent：使用Node Manager
- Agent可以用`Node Manager`管理，也可以直接启动
- `Node Manager`的文件在`C:\Oracle\Middleware\Oracle_Home\user_projects\domains\base_domain\bin`下，也就是你的域的文件夹下。运行`startNodeManager.cmd`即可
- 启动好`Node Manager`之后，运行`startComponent.cmd OracleDIAgent1`即可。注意后面区分大小写，且是Agent的名字

#4.启动Agent：不使用Node Manager
- 直接运行`agent.cmd -NAME=OracleDIAgent1`就行了


#5.其他
- `Node Manager`可以设置为服务，在`C:\Oracle\Middleware\Oracle_Home\user_projects\domains\base_domain\bin`下，有`installNodeMgrSvc`这个脚本。服务名称叫做`Oracle Weblogic base_domain NodeManager (C_Oracle_MIDDLE~1_ORACLE~1_wlserver)`
- 启动完成后，可以通过`https://127.0.0.1:5556/`访问Node Manager
- 每个Agent，都可以通过`http://localhost:20910/OracleDIAgentB`访问，如果这个打不开，Agent也打不开
- 如果忘了`Agent`的名字，在`C:\Oracle\Middleware\Oracle_Home\user_projects\domains\base_domain\system_components\ODI`下的目录下就是
- **注意不同的域下，启动脚本位置是不同的**

#6.TS
##证书问题（这个似乎还是有点问题）
- `NodeManager`的服务无法启动，运行之后就立刻退出。报错：
```
weblogic.nodemanager.common.ConfigException: Identity key store file not found: C:\Oracle\Middleware\Oracle_Home\user_projects\domains\base_domain\security\DemoIdentity.jks
```
- 看了下，确实没有这个`DemoIdentity.jks`文件，查了下，是`Weblogic`的证书Key文件
- 尝试了从其他服务器拿过来文件，`NodeManger`能启动了，但是`https://127.0.0.1:5556/`依旧无法打开，提示`:-ERR Error reading from socket: Unknown protocol exception`错误
- 因此需要拷贝`DemoIdentity.jks`和`DemoTrust.jks`两个文件：他们是一对的

##物理代理中的数据源
- ODI新建物理代理的时候不需要设置数据源，不要画蛇添足，否则就像这样：
```
2018-02-22 22:53:35.479 ERROR ODI-1419 连接到代理ODIAgentA时出现警告: 连接到工作资料档案库WORKREPO时出现 JDBC 连接错误。
2018-02-22 22:53:35.651 NOTIFICATION Ignoring DataSource customization because provider class was not DriverManagerDataSourceProvider
2018-02-22 22:53:35.651 WARNING ODI-1436 检索资料档案库WORKREPO的 ID 统计信息时出错。
2018-02-22 22:53:35.666 NOTIFICATION ODI-1111 代理ODIAgentA已启动。代理版本: 12.2.1。端口: 20910。JMX 端口: 21910。
2018-02-22 22:53:35.666 NOTIFICATION ODI-1136 在代理ODIAgentA上启动调度程序。
2018-02-22 22:53:35.979 NOTIFICATION Ignoring DataSource customization because provider class was not DriverManagerDataSourceProvider
2018-02-22 22:53:35.979 WARNING ODI-2006 计算工作资料档案库 [WORKREPO] 的调度时出错。将以 30 秒间隔重复此操作, 直到成功 。错误消息:ODI-10181: 未分类的配置异常错误。
ODI-10143: 访问WORK资料档案库时出错。
javax.naming.NameNotFoundException; remaining name 'jdbc/odiWorkRepository'
2018-02-22 22:53:35.979 INCIDENT_ERROR ODI-1131 代理ODIAgentA遇到错误: ODI-1428: 内部错误 Caused by: ODI-10181: 未分类的配置异常错误。
ODI-10143: 访问WORK资料档案库时出错。
```
解决：吧数据源删掉就好了（留空）









