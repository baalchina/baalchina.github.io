BBR，`Bottleneck Bandwidth and RTT`，大致理解为在拥塞网络下能表现很好的一个协议就好了。干吗用的？高大上用在数据中心互联，我们就fq呗...
配置很简单，需要注意几点：
- Linode的VPS需要是KVM的，我的以前是Xen的，死活不行，干掉换成KVM的就好了
- 参考这个：https://www.linode.com/docs/tools-reference/custom-kernels-distros/run-a-distribution-supplied-kernel-with-kvm，首先得把Linode的内核换成非自定义内核
- 再安装4.9的内核，配置一番即可，参考：http://www.linuxeye.com/Linux/Linode-CentOS7-Google-BBR.html

开启TCP-BBR
```
cat >>/etc/sysctl.conf << EOF
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
EOF
```
内核参数生效：

- sysctl -p 生效
查看bbr是否生效：

```
[root@linode1495332 ~]# sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno
[root@linode1495332 ~]# lsmod | grep bbr
tcp_bbr                16384  70
```


配置完成后，看4K的Youtube都很流畅，以前Linode的vps，跑个google网页都经常跑不动...