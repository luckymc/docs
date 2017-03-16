### PHP中的Mysql查询

##### 1. 字符编码utf8
连接db时，设置字符编码为utf8

```
$pdo = new PDO('mysql:host=localhost;dbname=test;charset=utf8', 'root', 'root');
```

##### 2. 查询结果使用关联数组

```
$pdo->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
```