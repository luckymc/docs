### Linux常用命令

1. 重置用户密码
```
passwd username
```

2. 查看系统信息
```
uname -a
cat /proc/version
```

3. 将当前目录(包括子目录)中所有txt文件中的yyyy字符串替换为xxxx字符串
```
sed -i s/yyyy/xxxx/g `grep yyyy -rl --include="*.txt" ./
```

4. CRUL查看响应头信息
```
-H: 添加Header信息
-d: POST参数
-v: 包含响应头信息
-I: 仅返回响应头信息
```