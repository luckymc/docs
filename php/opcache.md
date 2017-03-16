### opcache笔记

查看opcache状态
```
php -i |grep opcache

// 结果如下，可以看出opcache.enable => On，处于开启状态
Configure Command =>  './configure'  '--prefix=/usr/local/anjuke-php-fpm' '--with-config-file-path=/usr/local/anjuke-php-fpm/etc' '--with-config-file-scan-dir=/usr/local/anjuke-php-fpm/etc/conf.d' '--enable-opcache' '--enable-fpm' '--enable-calendar' '--enable-ftp' '--with-gmp' '--with-openssl' '--enable-pcntl' '--enable-shmop' '--enable-sysvmsg' '--enable-sysvsem' '--enable-wddx' '--with-xsl' '--enable-bcmath' '--with-libxml-dir' '--enable-mbstring' '--enable-sockets' '--enable-zip' '--with-zlib' '--with-mcrypt' '--enable-exif' '--with-curl' '--enable-mysqlnd' '--with-pdo-mysql=mysqlnd' '--with-mysqli=mysqlnd' '--with-mysql=mysqlnd' '--with-gd' '--with-vpx-dir' '--with-jpeg-dir' '--with-png-dir' '--with-zlib-dir' '--with-tidy' '--with-xpm-dir' '--with-freetype-dir' '--enable-gd-native-ttf' '--with-gettext' '--with-bz2'
/usr/local/anjuke-php-fpm/etc/conf.d/opcache.ini,
opcache.blacklist_filename => no value => no value
opcache.consistency_checks => 0 => 0
opcache.dups_fix => Off => Off
opcache.enable => On => On
opcache.enable_cli => Off => Off
opcache.enable_file_override => Off => Off
```

关闭opcache
```
1. 打开opcache配置文件，如上：
vi /usr/local/anjuke-php-fpm/etc/conf.d/opcache.ini

2. 注释掉
;zend_extension=opcache.so
;opcache.enable=1
;opcache.enable_cli=0  //disable php_cli
;opcache.memory_consumption=256      //共享内存大小, 这个根据你们的需求可调
;opcache.interned_strings_buffer=16   //interned string的内存大小, 也可调
;opcache.max_accelerated_files=40000  //最大缓存的文件数目
;opcache.revalidate_freq=60           //60s检查一次文件更新
;opcache.fast_shutdown=1
;opcache.save_comments=0              //不保存文件/函数的注释

3. 重启PHP
/etc/init.d/anjuke-php-fpm reload
```