其实只是想翻回单位方便干活而已...

#服务器准备工作

##准备源
`# yum install epel-release`
##安装OpenVPN和EasyRSA
`# yum install -y openvpn easy-rsa`
##修改配置文件
`cp /usr/share/doc/openvpn-*/sample/sample-config-files/server.conf /etc/openvpn`
##修改`/etc/openvpn/server.conf`的内容
```
dh dh2048.pem
redirect-gateway def1 bypass-dhcp” //去掉注释
push “redirect-gateway def1 bypass-dhcp”
push “dhcp-option DNS 210.28.92.7” //改成单位的DNS
user nobody
group nobody
```
这里需要注意的是`server`的配置，你需要根据你的网络情况来。例如你的内网是10.0.0.0/8，你就不能用默认的10地址，最好改成192.168.地址


##创建证书
```
# mkdir -p /etc/openvpn/easy-rsa/keys
# cp -rf /usr/share/easy-rsa/2.0/* /etc/openvpn/easy-rsa
# cp /etc/openvpn/easy-rsa/openssl-1.0.0.cnf /etc/openvpn/easy-rsa/openssl.cnf
```

```
# cd /etc/openvpn/easy-rsa
# source ./vars
# ./clean-all
# ./build-ca
# ./build-key-server server
# ./build-dh
```

```
# cd /etc/openvpn/easy-rsa/keys
# cp dh2048.pem ca.crt server.crt server.key /etc/openvpn
```

##配置路由和防火墙
启用防火墙
```
#systemctl status firewalld.service
# firewall-cmd --list-services
dhcpv6-client http https ssh
```
测试防火墙配置
```
# firewall-cmd --add-service openvpn
success
# firewall-cmd --permanent --add-service openvpn
success
```

```
# firewall-cmd --add-masquerade
success
# firewall-cmd --permanent --add-masquerade
success
```
##允许Ip转发
```
vim /etc/sysctl.conf

# Controls IP packet forwarding
net.ipv4.ip_forward = 1
```

##启动OpenVPN
```
sysctl -p
systemctl start openvpn@server
systemctl enable openvpn@server
```
#本地Client配置（Windows
配置一个配置文件
```
client
dev tun
#这个就是你的虚拟网卡的名字
dev-node vpn
--ncp-disable
proto udp
remote your-server-ip 1194
remote-cert-tls server
tun-mtu 1500
resolv-retry infinite
nobind
persist-key
persist-tun
cipher AES-256-CBC
keysize 256
verb 3
ca C:\\Users\\baalchina\\Desktop\\keys\\ca.crt
cert C:\\Users\\baalchina\\Desktop\\keys\\client.crt
key C:\\Users\\baalchina\\Desktop\\keys\\client.key
dh C:\\Users\\baalchina\\Desktop\\keys\\dh2048.pem
```

#然后
然后就没有然后了，Enjoy吧