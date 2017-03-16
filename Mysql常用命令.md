### Mysql常用命令

1.备份
```
mysqldump -h localhost -uroot -proot user > /home/user.sql
```
ps：密码中如果有特殊字符，需要转义，如'('需要转义成'\\('

2.设置auto_increment
```
alter table user auto_increment = 1000;
```