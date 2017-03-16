### Mysql远程访问开启

Mysql开启远程访问需要同时满足一下两个条件：
1. 数据库用户名允许外网IP访问
2. 服务器允许外网IP访问

> 以下假设Mysql服务器地址为192.168.1.10，端口为3306

**数据库设置**
1. 添加外网数据库使用的用户名和密码,并赋予外网可访问的权限

```
#假设用户名为write，密码为write，%代表任何IP都可以访问
grant all on *.* to 'write'@'%' identified by 'write';
```
2. 确认my.cnf配置（之前遇到的一个坑）

```
#注释掉下面这行配置，或者修改为远程的服务器IP
#bind-address       = 127.0.0.1
```

**防火墙端口开启**

可以通过telnet确认3306端口是否开启

```
telnet 192.168.1.10 3306
```

如果未开启，可以按照以下方法开启。

1. 执行 vi /etc/sysconfig/iptables
```
# Firewall configuration written by system-config-securitylevel
# Manual customization of this file is not recommended.
*filter
:INPUT DROP [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:syn-flood - [0:0]
-A INPUT -i lo -j ACCEPT
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 21 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
# 加入下面这行，开启3306端口
-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 3690 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 20000:30000 -j ACCEPT
-A INPUT -p icmp -m limit --limit 100/sec --limit-burst 100 -j ACCEPT
-A INPUT -p icmp -m limit --limit 1/s --limit-burst 10 -j ACCEPT
-A INPUT -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j syn-flood
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A syn-flood -p tcp -m limit --limit 3/sec --limit-burst 6 -j RETURN
-A syn-flood -j REJECT --reject-with icmp-port-unreachable
COMMIT
```


2. 重启iptables

```
service iptables restart
或者
/etc/init.d/iptables restart
```

下面可以试着在远程服务器上连接Mysql了

```
mysql -h 192.168.1.10 -P3306 -uwrite -p
```
