Windows下使用Let's Encrypt证书就稍微麻烦一点，注意几个坑

- 工具可以用`letsencrypt-win-simple`（`https://github.com/Lone-Coder/letsencrypt-win-simple`)
- 命令：`letsencrypt.exe --accepttos --manualhost your.host.com --webroot C:\Program Files\Update Services\WebServices\Root\`
- 会生成几个文件，在`c:\program`下，Let's Encypty服务器需要能访问你的目录，比如`http://your.host.com/.well-known/acme-challenge/d131231ead31re12`
- 所以你需要建立一个虚拟目录叫做`.well-known`。直接建目录是不行的，Windows不支持.开头的目录
- MIME类型，需要新增一个.的，类型是`text/plain`
- 建完了自己用浏览器访问以下看是否可以打开
- 然后就可以申请了。服务器有一个限制，每小时/单域名/不能超过5次失败。所以失败过多就等会再说吧
- 证书有效期90天，所以它会自动建一个计划任务，定期执行（60天）