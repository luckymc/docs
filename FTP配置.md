### FTP配置

1. 安装vsftpd服务

```
sudo apt-get install vsftpd
```

2、打开/etc/vsftpd.conf

取消如下行的注释（行号为29和33）

```
write_enable=YES
local_umask=022
```

取消如下行的注释（行号120）来阻止除了用户文件夹意外的文件夹。
```
chroot_local_user=YES
```

在文件最后增加如下一行：
```
allow_writeable_chroot=YES
```

添加如下行开启消极模式
```
pasv_enable=Yes
pasv_min_port=40000
pasv_max_port=40100
```




3. 用如下命令重启vsftpd服务
```
sudo service vsftpd restart
```

4. 开启端口
```
iptables -I INPUT 5 -p tcp --dport 21 -j ACCEPT

service vsftpd restart

ufw allow 21

ufw reload
```

5. 添加用户
```
sudo useradd -m username -s /bin/shell
sudo passwd pwd
```