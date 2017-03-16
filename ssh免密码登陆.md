### ssh免密码登陆

有机器A(192.168.1.1)，B(192.168.1.2)。现想A通过ssh免密码登录到B。

1. 在A机生成公钥/私钥对
```
ssh-keygen -t rsa -P ''

-P表示密码，-P '' 就表示空密码，也可以不用-P参数，这样就要三车回车，用-P就一次回车。

~/.ssh下生成id_rsa和id_rsa.pub。
```
2. 把A机下的id_rsa.pub复制到B机下，在B机的.ssh/authorized_keys文件里

3. 修改authorized_keys的权限为600
```
chmod 600 authorized_keys
```

4. 这样就可以在A机免密码登陆到B机了