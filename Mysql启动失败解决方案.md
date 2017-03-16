### Mysql启动失败

启动命令如下
```
mysqld_safe
或者
mysql.server start
```

报错信息
```
140131 00:03:02 mysqld_safe Starting mysqld daemon with databases from /usr/local/var/mysql
2014-01-31 00:03:03 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
2014-01-31 00:03:03 13223 [Warning] Setting lower_case_table_names=2 because file system for /usr/local/var/mysql/ is case insensitive
2014-01-31 00:03:03 13223 [Note] Plugin 'FEDERATED' is disabled.
/usr/local/Cellar/mysql/5.6.15/bin/mysqld: Can't find file: './mysql/plugin.frm' (errno: 13 - Permission denied)
2014-01-31 00:03:03 13223 [ERROR] Can't open the mysql.plugin table. Please run mysql_upgrade to create it.
2014-01-31 00:03:03 13223 [Note] InnoDB: The InnoDB memory heap is disabled
2014-01-31 00:03:03 13223 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
2014-01-31 00:03:03 13223 [Note] InnoDB: Compressed tables use zlib 1.2.3
2014-01-31 00:03:03 13223 [Note] InnoDB: Using CPU crc32 instructions
2014-01-31 00:03:03 13223 [Note] InnoDB: Initializing buffer pool, size = 128.0M
2014-01-31 00:03:03 13223 [Note] InnoDB: Completed initialization of buffer pool
2014-01-31 00:03:03 13223 [ERROR] InnoDB: ./ibdata1 can't be opened in read-write mode
2014-01-31 00:03:03 13223 [ERROR] InnoDB: The system tablespace must be writable!
2014-01-31 00:03:03 13223 [ERROR] Plugin 'InnoDB' init function returned error.
2014-01-31 00:03:03 13223 [ERROR] Plugin 'InnoDB' registration as a STORAGE ENGINE failed.
2014-01-31 00:03:03 13223 [ERROR] Unknown/unsupported storage engine: InnoDB
2014-01-31 00:03:03 13223 [ERROR] Aborting

2014-01-31 00:03:03 13223 [Note] Binlog end
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'partition'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'PERFORMANCE_SCHEMA'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_DATAFILES'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_TABLESPACES'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_FOREIGN_COLS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_FOREIGN'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_FIELDS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_COLUMNS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_INDEXES'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_TABLESTATS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_SYS_TABLES'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_FT_INDEX_TABLE'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_FT_INDEX_CACHE'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_FT_CONFIG'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_FT_BEING_DELETED'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_FT_DELETED'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_FT_DEFAULT_STOPWORD'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_METRICS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_BUFFER_POOL_STATS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_BUFFER_PAGE_LRU'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_BUFFER_PAGE'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_CMP_PER_INDEX_RESET'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_CMP_PER_INDEX'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_CMPMEM_RESET'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_CMPMEM'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_CMP_RESET'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_CMP'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_LOCK_WAITS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_LOCKS'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'INNODB_TRX'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'BLACKHOLE'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'ARCHIVE'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'MRG_MYISAM'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'MyISAM'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'MEMORY'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'CSV'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'sha256_password'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'mysql_old_password'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'mysql_native_password'
2014-01-31 00:03:03 13223 [Note] Shutting down plugin 'binlog'
2014-01-31 00:03:03 13223 [Note] /usr/local/Cellar/mysql/5.6.15/bin/mysqld: Shutdown complete

140131 00:03:03 mysqld_safe mysqld from pid file /usr/local/var/mysql/chengl-macbook.local.pid ended
```

解决方案

删除.err文件，然后重新启动

```
rm /usr/local/var/mysql/chengl-macbook.local.err
```