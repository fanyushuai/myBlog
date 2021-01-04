title: mysql
author: John Doe
tags:
  - mysql 语句
  - ''
categories:
  - mysql
date: 2019-10-28 13:46:00
---
# 1.mysql 按in条件中的字段排序
 ```
SELECT * FROM 表名 WHERE id in(值) order by field(字段,值);
```

# 2.查询按照分组将多条记录转换成单条记录的
```
group_concat([DISTINCT] 要连接的字段 [Order BY ASC/DESC 排序字段][Separator '分隔符'])
```
查询后字段是有长度的，可以执行以下语句进行查询:
```
show variables like 'group_concat_max_len';
```
修改的方式有两种：

(1).在my.ini [mysql]后面加入 （需重启）：
```
group_concat_max_len = 102400000';
```
    
(2).执行以下语句（重启失效）：
```
SET GLOBAL group_concat_max_len = 1024000;
```
# 3.This function has none of DETERMINISTIC, NO SQL
```
SET GLOBAL log_bin_trust_function_creators = 1;
```
# 4.锁表有关
  -- 查询是否锁表
```
SHOW OPEN TABLES WHERE In_use > 0;
```

-- 查看所有进程
```
SHOW PROCESSLIST;
SHOW FULL PROCESSLIST;
```

  -- 杀掉指定mysql连接的进程号
```
KILL 178;
```

  -- 拼写多个时间大于x的kill语句
```
SELECT CONCAT('kill ', id,';') FROM information_schema.PROCESSLIST WHERE time > 100;
```

  -- 查看正在锁的事务
```
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS;
```

  -- 查看等待锁的事务
```
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCK_WAITS;
```

  -- 查看innodb引擎的运行时信息
```
SHOW engine innodb status;
```

  -- 查看造成死锁的sql语句，分析索引情况，然后优化sql语句

  -- 查看服务器状态
```
SHOW STATUS LIKE '%lock%';
```

  -- 查看超时时间：
```
SHOW VARIABLES LIKE '%timeout%';
```

  -- 拼写多个被锁的kill语句
```
select concat('kill ', id,';') from information_schema.processlist where state like '%Locked%';
```
# 5.uuid()
```
CREATE DEFINER=`root`@`%` FUNCTION `getUUID`() RETURNS varchar(50) CHARSET utf8
BEGIN
	DECLARE uuid varchar(50);
	select concat(DATE_FORMAT(NOW(),'%Y%m%d%H%i%s'),replace(uuid(),'-','')) from dual INTO uuid;
	RETURN uuid;
END 
```
# 6.哪些表有大于N条数据
```
USE information_schema;
SELECT TABLE_NAME ,TABLE_ROWS FROM TABLES WHERE TABLE_SCHEMA='库名' AND TABLE_ROWS > N ORDER BY TABLE_ROWS DESC; 
```
