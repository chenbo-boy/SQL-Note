# SQL-Note2 SQL语法学习
##### MySql-SQL语法
## 目录
+ [数据库(模式schema)](#数据库)
  + [查看所有数据库]
  + [查看指定数据库中的表]
  + [切换数据库]
+ [表操作](#表操作)
  + [mySql数据库数据类型](#mySql数据库数据类型)
  + [创建表](#创建表)
  + [插入数据](#插入数据)
  + [查询](#查询)
    + [查询表结构](嵌套查询)
    + [查询建表语句](查询建表语句)
    + [一般查询格式](#一般查询格式)
    + [ALL|DISTINCT](ALL|DISTINCT)
    + [条件查询](#条件查询)
      + [比较运算符](比较运算符)
      + [确定范围](确定范围)
        + [BETWEEN AND](BETWEEN AND)
        + [NOT BETWEEN AND](NOT BETWEEN AND)
      + [确定集合](确定集合)
        + [IN](IN)
        + [NOT IN](NOT IN)
      + [字符匹配](字符匹配)
        + [LIKE](LIKE)
        + [NOT LIKE](NOT LIKE)
        + [REGEXP | RLIKE](REGEXP | RLIKE)
        + [NOT REGEXP | NOT RLIKE](NOT REGEXP | NOT RLIKE)
      + [空值](空值)
        + [IS NULL](空值)
        + [IS NOT NULL](IS NOT NULL)
      + [逻辑运算](逻辑运算)
        + [AND](ADD)
        + [OR](OR)
        + [NOT](NOT)
      + [UNION](UNION)
      + [UNION ALL](UNION ALL)
      + [LIMIT](LIMIT)
      + [别名](别名)
        + [CONCAT](CONCAT)
    + [嵌套查询](嵌套查询)
    + [连接查询](连接查询)
    + [排序](排序)
      + [ASC]
      + [DESC]
    + [分组](分组)
   + [更新](#更新)
   + [删除](#删除)
   + [修改表结构](#修改表结构)
+ [视图](视图)
+ [索引](索引)
+ [函数](函数)
+ [CHEC约束](CHEC约束)
+ [触发器](触发器)
+ [权限控制](权限控制)

### 数据库
#### 查看所有数据库
SQL创建表语句的一般格式：
SHOW DATABASES;

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| my_db              |
| mysql              |
| performance_schema |
| sakila             |
| student            |
| sys                |
| test               |
| world              |
+--------------------+
9 rows in set (0.01 sec)
```

#### 查看指定数据库中的表 
    其实所有表和数据库的信息都在information_schema库里。看一下这个库里的所有表。
    
```
mysql> use information_schema;
Database changed
mysql> show tables;
+---------------------------------------+
| Tables_in_information_schema          |
+---------------------------------------+
| CHARACTER_SETS                        |
| COLLATION_CHARACTER_SET_APPLICABILITY |
| COLLATIONS                            |
| COLUMN_PRIVILEGES                     |
| COLUMN_STATISTICS                     |
| COLUMNS                               |
| ENGINES                               |
| EVENTS                                |
| FILES                                 |
| INNODB_BUFFER_PAGE                    |
| INNODB_BUFFER_PAGE_LRU                |
| INNODB_BUFFER_POOL_STATS              |
| INNODB_CACHED_INDEXES                 |
| INNODB_CMP                            |
| INNODB_CMP_PER_INDEX                  |
| INNODB_CMP_PER_INDEX_RESET            |
| INNODB_CMP_RESET                      |
| INNODB_CMPMEM                         |
| INNODB_CMPMEM_RESET                   |
| INNODB_COLUMNS                        |
| INNODB_DATAFILES                      |
| INNODB_FIELDS                         |
| INNODB_FOREIGN                        |
| INNODB_FOREIGN_COLS                   |
| INNODB_FT_BEING_DELETED               |
| INNODB_FT_CONFIG                      |
| INNODB_FT_DEFAULT_STOPWORD            |
| INNODB_FT_DELETED                     |
| INNODB_FT_INDEX_CACHE                 |
| INNODB_FT_INDEX_TABLE                 |
| INNODB_INDEXES                        |
| INNODB_METRICS                        |
| INNODB_SESSION_TEMP_TABLESPACES       |
| INNODB_TABLES                         |
| INNODB_TABLESPACES                    |
| INNODB_TABLESPACES_BRIEF              |
| INNODB_TABLESTATS                     |
| INNODB_TEMP_TABLE_INFO                |
| INNODB_TRX                            |
| INNODB_VIRTUAL                        |
| KEY_COLUMN_USAGE                      |
| KEYWORDS                              |
| OPTIMIZER_TRACE                       |
| PARAMETERS                            |
| PARTITIONS                            |
| PLUGINS                               |
| PROCESSLIST                           |
| PROFILING                             |
| REFERENTIAL_CONSTRAINTS               |
| RESOURCE_GROUPS                       |
| ROUTINES                              |
| SCHEMA_PRIVILEGES                     |
| SCHEMATA                              |
| ST_GEOMETRY_COLUMNS                   |
| ST_SPATIAL_REFERENCE_SYSTEMS          |
| STATISTICS                            |
| TABLE_CONSTRAINTS                     |
| TABLE_PRIVILEGES                      |
| TABLES                                |
| TABLESPACES                           |
| TRIGGERS                              |
| USER_PRIVILEGES                       |
| VIEW_ROUTINE_USAGE                    |
| VIEW_TABLE_USAGE                      |
| VIEWS                                 |
+---------------------------------------+
65 rows in set (0.02 sec)

数据库下面的所有表信息都在TABLES表里，看下TABLES表信息：
mysql> desc TABLES;
+-----------------+--------------------------------------------------------------------+------+-----+---------+-------+
| Field           | Type                                                               | Null | Key | Default | Extra |
+-----------------+--------------------------------------------------------------------+------+-----+---------+-------+
| TABLE_CATALOG   | varchar(64)                                                        | YES  |     | NULL    |       |
| TABLE_SCHEMA    | varchar(64)                                                        | YES  |     | NULL    |       |
| TABLE_NAME      | varchar(64)                                                        | YES  |     | NULL    |       |
| TABLE_TYPE      | enum('BASE TABLE','VIEW','SYSTEM VIEW')                            | NO   |     | NULL    |       |
| ENGINE          | varchar(64)                                                        | YES  |     | NULL    |       |
| VERSION         | int(2)                                                             | YES  |     | NULL    |       |
| ROW_FORMAT      | enum('Fixed','Dynamic','Compressed','Redundant','Compact','Paged') | YES  |     | NULL    |       |
| TABLE_ROWS      | bigint(21) unsigned                                                | YES  |     | NULL    |       |
| AVG_ROW_LENGTH  | bigint(21) unsigned                                                | YES  |     | NULL    |       |
| DATA_LENGTH     | bigint(21) unsigned                                                | YES  |     | NULL    |       |
| MAX_DATA_LENGTH | bigint(21) unsigned                                                | YES  |     | NULL    |       |
| INDEX_LENGTH    | bigint(21) unsigned                                                | YES  |     | NULL    |       |
| DATA_FREE       | bigint(21) unsigned                                                | YES  |     | NULL    |       |
| AUTO_INCREMENT  | bigint(21) unsigned                                                | YES  |     | NULL    |       |
| CREATE_TIME     | timestamp                                                          | NO   |     | NULL    |       |
| UPDATE_TIME     | datetime                                                           | YES  |     | NULL    |       |
| CHECK_TIME      | datetime                                                           | YES  |     | NULL    |       |
| TABLE_COLLATION | varchar(64)                                                        | YES  |     | NULL    |       |
| CHECKSUM        | bigint(21)                                                         | YES  |     | NULL    |       |
| CREATE_OPTIONS  | varchar(256)                                                       | YES  |     | NULL    |       |
| TABLE_COMMENT   | varchar(256)                                                       | YES  |     | NULL    |       |
+-----------------+--------------------------------------------------------------------+------+-----+---------+-------+
21 rows in set (0.01 sec)

```
查看'test' schema中的所有表名称
方式一：
```
mysql> select TABLE_NAME from information_schema.TABLES where TABLE_SCHEMA='test';
+------------+
| TABLE_NAME |
+------------+
| custom     |
| product    |
+------------+
2 rows in set (0.01 sec)
```
方式二：
```
mysql> use test;
Database changed
mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| custom         |
| product        |
+----------------+
2 rows in set (0.00 sec)
```

#### 切换数据库
语法：use 数据库名称;
```
mysql> use test;
Database changed
```

### 表操作

#### mySql数据库数据类型
  [mySql数据库数据类型](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
  
#### 创建表
SQL创建表语句的一般格式：
CREATE TABLE <表名>
(<列名> <数据类型> [<列级完整性约束>]
[,<列名> <数据类型> [<列级完整性约束>]]...
[,<表级完整性约束>]);

数据类型:数据库系统支持的各种数据类型，包括长度和精度。
列级完整性约束：针对单个列，包括：PRIMARY KEY,REFERENCES,UNIQUE,NOT NULL等
表级完整性约束：针对多列，包括：PRIMARY KEY,FOREIGN REFERENCES等
```
CREATE TABLE IF NOT EXISTS `suser`(
   `id` INT NOT NULL UNIQUE AUTO_INCREMENT,
   `name` VARCHAR(20) NOT NULL DEFAULT '',
   `age` INT NOT NULL DEFAULT 0,
   `gender` INT NOT NULL DEFAULT 0,
   PRIMARY KEY ( `id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
ENGINE=InnoDB：指定表引擎为InnoDB，InnoDB引擎允许创建索引。
DEFAULT CHARSET=utf8：指定默认字符编码为utf8。

#### 插入数据
-- 指定列名，插入数据
INSERT INTO suser (name,age,gender) VALUES ('陈波',26,0);
-- 插入多个数据
INSERT INTO suser (name,age,gender) VALUES ('陈一',12,1),('陈二',15,1),('陈三',32,0);
-- 对于设置了自动增长的列，设值为0或null就可以自动增长，不用写出列名。
INSERT INTO suser VALUES (0,'陈四',26,0);

#### 查询
##### 查询表结构
方式一：
```
mysql> desc table_name;
```
方式二：
```
mysql> show columns from table_name;
```
方式三：
```
mysql> use information_schema;
mysql> select * from columns where table_name='tabLe_name';
```
##### 查询建表语句
```
mysql> show create table suser;
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                                                                                                  |
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| suser | CREATE TABLE `suser` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL DEFAULT '',
  `age` int(11) NOT NULL DEFAULT '0',
  `gender` int(11) NOT NULL DEFAULT '0',
  PRIMARY KEY (`id`),
  UNIQUE KEY `id` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8 |
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.01 sec)
```
##### 一般查询格式
SQL查询语句的一般格式：
```
SELECT [ALL|DISTINCT] <算术表达式列表> FROM <表名或视图名列表>
[WHERE <条件表达式1>]
[GROUP BY <属性列表1> [HAVING <条件表达式2>]]
[ORDER BY <属性列表2> [ASC | DESC]];
```
+--------------+--------------------------------+
|    查询条件   |      运算符/谓词                |
+--------------+----------+------------+--------+
|      比较     | =,>,<,>=,<=,!=,<>,!>,!<        |
+--------------+--------------------------------+
|    确定范围   | BETWEEN AND,NOT BETWEEN AND    |
+--------------+--------------------------------+
|    确定集合   | IN，NOT IN ,ANY,SOME           |
+--------------+--------------------------------+
|    字符匹配   | LIKE,NOT LIKE                  |
+--------------+--------------------------------+
|     空 值     | IS NULL,IS NOT NULL            |
+--------------+--------------------------------+
|    逻辑运算   | AND,OR,NOT                     |
+--------------+--------------------------------+


--显示数据的全部字段
SELECT * FROM 表名；
--显示指定字段数据
SELECT column_name1,column_name2,... FROM 表名;
--查询多个表数据
```
mysql> select * from city ci,countrylanguage co where ci.CountryCode='CHN' AND co.CountryCode='CHN' LIMIT 5;
+------+-----------+-------------+-----------+------------+-------------+----------+------------+------------+
| ID   | Name      | CountryCode | District  | Population | CountryCode | Language | IsOfficial | Percentage |
+------+-----------+-------------+-----------+------------+-------------+----------+------------+------------+
| 1890 | Shanghai  | CHN         | Shanghai  |    9696300 | CHN         | Chinese  | T          |       92.0 |
| 1891 | Peking    | CHN         | Peking    |    7472000 | CHN         | Chinese  | T          |       92.0 |
| 1892 | Chongqing | CHN         | Chongqing |    6351600 | CHN         | Chinese  | T          |       92.0 |
| 1893 | Tianjin   | CHN         | Tianjin   |    5286800 | CHN         | Chinese  | T          |       92.0 |
| 1894 | Wuhan     | CHN         | Hubei     |    4344600 | CHN         | Chinese  | T          |       92.0 |
+------+-----------+-------------+-----------+------------+-------------+----------+------------+------------+
5 rows in set (0.00 sec)

mysql> select * from city limit 1;
+----+-------+-------------+----------+------------+
| ID | Name  | CountryCode | District | Population |
+----+-------+-------------+----------+------------+
|  1 | Kabul | AFG         | Kabol    |    1780000 |
+----+-------+-------------+----------+------------+
1 row in set (0.00 sec)

mysql> select * from countrylanguage limit 1;
+-------------+----------+------------+------------+
| CountryCode | Language | IsOfficial | Percentage |
+-------------+----------+------------+------------+
| ABW         | Dutch    | T          |        5.3 |
+-------------+----------+------------+------------+
1 row in set (0.00 sec)
```
##### ALL|DISTINCT  
默认ALL显示全部数据，DISTINCT:过滤重复数据。

##### 条件查询
###### 比较运算符

--查询条件：>=
--查询国家土地面积大于等于9572900的国家
```
mysql> select Code,Name,SurfaceArea from country where SurfaceArea>=9572900;
+------+--------------------+-------------+
| Code | Name               | SurfaceArea |
+------+--------------------+-------------+
| ATA  | Antarctica         | 13120000.00 |
| CAN  | Canada             |  9970610.00 |
| CHN  | China              |  9572900.00 |
| RUS  | Russian Federation | 17075400.00 |
+------+--------------------+-------------+
4 rows in set (0.01 sec)
```

###### 确定范围
###### BETWEEN AND
--BETWEEN
--查询年龄在20-40岁之间并按年龄升序排序
```
mysql> select * from suser where age BETWEEN 20 AND 40 ORDER BY age ASC;
+----+------+-----+--------+
| id | name | age | gender |
+----+------+-----+--------+
|  1 | 陈波 |  26 |      0 |
|  5 | 陈四 |  26 |      0 |
|  6 | 王一 |  26 |      0 |
|  4 | 陈三 |  32 |      0 |
+----+------+-----+--------+
4 rows in set (0.00 sec)
```
###### NOT BETWEEN AND

--查询年龄不在20-40岁之间并按年龄升序排序
```
mysql> select * from suser where age NOT BETWEEN 20 AND 40 ORDER BY age ASC;
+----+--------+-----+--------+
| id | name   | age | gender |
+----+--------+-----+--------+
|  9 | 陈嫣玉 |   0 |      1 |
|  2 | 陈一   |  12 |      1 |
|  3 | 陈二   |  15 |      1 |
|  8 | 王语嫣 |  18 |      1 |
|  7 | 王二   |  57 |      0 |
+----+--------+-----+--------+
5 rows in set (0.00 sec)
```
###### 确定集合
###### IN

--IN
--查询性别为女性的所有用户
```
mysql> select * from suser where gender in (select gender from suser where gender='1');
+----+--------+-----+--------+
| id | name   | age | gender |
+----+--------+-----+--------+
|  2 | 陈一   |  12 |      1 |
|  3 | 陈二   |  15 |      1 |
|  8 | 王语嫣 |  18 |      1 |
|  9 | 陈嫣玉 |   0 |      1 |
+----+--------+-----+--------+
4 rows in set (0.00 sec)
```

###### NOT IN
###### 字符匹配
###### LIKE

--字符匹配
|通配符	| 描述
|--------------------------------------
|%	替代 0 个或多个字符
|--------------------------------------
|_	替代一个字符
|--------------------------------------
|[charlist]	字符列中的任何单一字符
|--------------------------------------
|[^charlist]
|或
|[!charlist]	不在字符列中的任何单一字符

###### NOT LIKE
###### REGEXP | RLIKE
###### NOT REGEXP | NOT RLIKE

MySQL 中使用 REGEXP 或 NOT REGEXP 运算符 (或 RLIKE 和 NOT RLIKE) 来操作正则表达式。

--查询name以嫣结尾的数据
```
mysql> SELECT * from suser where name rlike '[嫣]$';
+----+--------+-----+--------+
| id | name   | age | gender |
+----+--------+-----+--------+
|  8 | 王语嫣 |  18 |      1 |
+----+--------+-----+--------+
1 row in set (0.00 sec)

mysql> SELECT * from suser where name REGEXP '[嫣]$';
+----+--------+-----+--------+
| id | name   | age | gender |
+----+--------+-----+--------+
|  8 | 王语嫣 |  18 |      1 |
+----+--------+-----+--------+
1 row in set (0.00 sec)
```
###### 空值
###### IS NULL
###### IS NOT NULL

--NULL使用
判断是否为空,IS NULL
判断不为空,IS NOT NULL

###### 逻辑运算
###### AND
###### OR
###### NOT
###### UNION

--UNION
UNION 操作符用于合并两个或多个 SELECT 语句的结果集，去除重复数据。

请注意，UNION 内部的每个 SELECT 语句的结果必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。
```
mysql> select * from suser UNION select * from course;
ERROR 1222 (21000): The used SELECT statements have a different number of columns
```
分析：select * from suser有4个列，select * from course有3个列。
```
mysql> use student;
Database changed
mysql> select * from suser;
+----+--------+-----+--------+
| id | name   | age | gender |
+----+--------+-----+--------+
|  1 | 陈波   |  26 |      0 |
|  2 | 陈一   |  12 |      1 |
|  3 | 陈二   |  15 |      1 |
|  4 | 陈三   |  32 |      0 |
|  5 | 陈四   |  26 |      0 |
|  6 | 王一   |  26 |      0 |
|  7 | 王二   |  57 |      0 |
|  8 | 王语嫣 |  18 |      1 |
|  9 | 陈嫣玉 |   0 |      1 |
| 10 |        |  40 |      1 |
+----+--------+-----+--------+
10 rows in set (0.01 sec)

mysql> select * from course;
+----+------+------+
| id | s_id | name |
+----+------+------+
|  1 |    1 | 数学 |
|  2 |    1 | 语文 |
|  3 |    1 | 英语 |
|  4 |    8 | 数学 |
|  5 |    8 | 历史 |
|  6 |    8 | 政治 |
|  7 |    2 | 数学 |
|  8 |    3 | 语文 |
|  9 |    5 | 英语 |
| 10 |    5 | 数学 |
| 11 |    2 | 历史 |
| 12 |    4 | 政治 |
+----+------+------+
12 rows in set (0.00 sec)

mysql> select id from suser UNION select s_id from course;
+----+
| id |
+----+
|  1 |
|  2 |
|  3 |
|  4 |
|  5 |
|  6 |
|  7 |
|  8 |
|  9 |
| 10 |
+----+
10 rows in set (0.01 sec)
```
###### UNION ALL

--UNION ALL
UNION ALL 操作符用于合并两个或多个 SELECT 语句的结果集，有重复数据。
CREATE TABLE IF NOT EXISTS `score`(
   `id` int not null UNIQUE AUTO_INCREMENT,
   `s_id` int not null,
   `s_name` varchar(20),
   `c_name` varchar(20),
   primary KEY (`id`),
   KEY `s_id` (`s_id`),
   CONSTRAINT `score_ibfk_2` FOREIGN KEY (`s_id`) REFERENCES `suser` (`id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO score VALUES (0,1,'陈波','数学'),(0,1,'陈波','语文'),(0,1,'陈波','英语'),(0,8,'王语嫣','历史');

表中没有分数字段，修改表结构增加分数字段：
ALTER TABLE score ADD num FLOAT(4,1);//四位数字，保留一位小数
插入分数：
UPDATE score SET num=90 where id=1;
```
mysql> select name from suser UNION select s_name from score;
+--------+
| name   |
+--------+
| 陈波   |
| 陈一   |
| 陈二   |
| 陈三   |
| 陈四   |
| 王一   |
| 王二   |
| 王语嫣 |
| 陈嫣玉 |
|        |
+--------+
10 rows in set (0.00 sec)

mysql> select name from suser UNION ALL select s_name from score;
+--------+
| name   |
+--------+
| 陈波   |
| 陈一   |
| 陈二   |
| 陈三   |
| 陈四   |
| 王一   |
| 王二   |
| 王语嫣 |
| 陈嫣玉 |
|        |
| 陈波   |
| 陈波   |
| 陈波   |
| 王语嫣 |
+--------+
14 rows in set (0.00 sec)
###### LIMIT
```
--limit
--查询定指条数记录
--查询年龄不在20-40岁之间并按年龄升序排序，只查询前3条数据
```
mysql> select * from suser where age NOT BETWEEN 20 AND 40 ORDER BY age ASC limit 3;
+----+--------+-----+--------+
| id | name   | age | gender |
+----+--------+-----+--------+
|  9 | 陈嫣玉 |   0 |      1 |
|  2 | 陈一   |  12 |      1 |
|  3 | 陈二   |  15 |      1 |
+----+--------+-----+--------+
3 rows in set (0.01 sec)

mysql> select * from suser where age NOT BETWEEN 20 AND 40 ORDER BY age ASC;
+----+--------+-----+--------+
| id | name   | age | gender |
+----+--------+-----+--------+
|  9 | 陈嫣玉 |   0 |      1 |
|  2 | 陈一   |  12 |      1 |
|  3 | 陈二   |  15 |      1 |
|  8 | 王语嫣 |  18 |      1 |
|  7 | 王二   |  57 |      0 |
+----+--------+-----+--------+
5 rows in set (0.00 sec)
```
###### 别名

--别名
--列的表名
--表的别名
```
mysql> select Name as 名称 ,District as 直辖市 ,Population as 人  from city limit 1;
+-------+--------+---------+
| 名称  | 直辖市 | 人      |
+-------+--------+---------+
| Kabul | Kabol  | 1780000 |
+-------+--------+---------+
1 row in set (0.01 sec)

mysql> select Name 名称 ,District 直辖市 ,Population 人  from city limit 1;
+-------+--------+---------+
| 名称  | 直辖市 | 人      |
+-------+--------+---------+
| Kabul | Kabol  | 1780000 |
+-------+--------+---------+
1 row in set (0.00 sec)
```
###### CONCAT

--CONCAT() as xxx
把多个字段联合起来给一个别名
--查询中国的上海市的人口，所属区域，所属州
```
mysql> select ci.Name 城市名称 ,District 直辖市 ,ci.Population 人口,concat(co.Continent,',',co.Region) 所属洲  from city ci,country co where ci.CountryCode='CHN' and Code='CHN' limit 1;
+----------+----------+---------+-------------------+
| 城市名称 | 直辖市   | 人口    | 所属洲            |
+----------+----------+---------+-------------------+
| Shanghai | Shanghai | 9696300 | Asia,Eastern Asia |
+----------+----------+---------+-------------------+
1 row in set (0.01 sec)
```

###### 嵌套查询

--嵌套查询
```
select * from countrylanguage where CountryCode in (select CountryCode from city limit 5) LIMIT 5;
ERROR 1235 (42000): This version of MySQL doesn't yet support 'LIMIT & IN/ALL/ANY/SOME subquery'
```
子查询语句中LIMIT和IN/ALL/ANY/SOME不能共存。就是(select CountryCode from city limit 5)不能存在limit.
解决办法：
1.给子查询语句再嵌套一层.
```
select * from countrylanguage where CountryCode in (select * from (select CountryCode from city limit 5) as cc) LIMIT 5;
```
2.去掉limit
```
select * from countrylanguage where CountryCode in (select CountryCode from city) LIMIT 5;
```

###### 连接查询

CREATE TABLE IF NOT EXISTS `course`(
   `id` INT NOT NULL UNIQUE AUTO_INCREMENT,
   `s_id` INT NOT NULL,
   `name` VARCHAR(20) NOT NULL DEFAULT '',
   PRIMARY KEY (`id`),
   KEY `s_id` (`s_id`),
   CONSTRAINT `COURSE_ibfk_1` FOREIGN KEY (`s_id`) REFERENCES `suser` (`id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
说明：
PRIMARY KEY (`id`)申明主键约束，
KEY `s_id` (`s_id`)建立索引，
CONSTRAINT `COURSE_ibfk_1` 申明约束,
FOREIGN KEY (`s_id`) REFERENCES `suser` (`id`) 申明外键s_id引用表suser中的id字段。


 插入数据：
 INSERT INTO course VALUES (0,1,'数学'),(0,1,'语文'),(0,1,'英语'),(0,8,'数学'),(0,8,'历史'),(0,8,'政治');
 INSERT INTO course VALUES (0,2,'数学'),(0,3,'语文'),(0,5,'英语'),(0,5,'数学'),(0,2,'历史'),(0,4,'政治');

    --JOIN 会把2个表的字段连接起来
    INNER JOIN:内连接,或等值连接,只返回左右2个表都匹配的行,不会出现NULL的字段。
    LEFT JOIN:左连接，左侧表全部返回，右侧表如果满足条件则返回匹配的行，不匹配则返回NULL。
    RIGHT JOIN:右连接，右侧表全部返回，左侧表如果满足条件则返回匹配的行，不匹配则返回NULL。
    FULL OUTER JOIN:关键字只要左表（table1）和右表（table2）其中一个表中存在匹配，就返回左右2个表中的数据.MySQL不支持。
```
mysql> select * from suser su INNER JOIN course co ON su.id = co.s_id;
+----+--------+-----+--------+----+------+------+
| id | name   | age | gender | id | s_id | name |
+----+--------+-----+--------+----+------+------+
|  1 | 陈波   |  26 |      0 |  1 |    1 | 数学 |
|  1 | 陈波   |  26 |      0 |  2 |    1 | 语文 |
|  1 | 陈波   |  26 |      0 |  3 |    1 | 英语 |
|  2 | 陈一   |  12 |      1 |  7 |    2 | 数学 |
|  2 | 陈一   |  12 |      1 | 11 |    2 | 历史 |
|  3 | 陈二   |  15 |      1 |  8 |    3 | 语文 |
|  4 | 陈三   |  32 |      0 | 12 |    4 | 政治 |
|  5 | 陈四   |  26 |      0 |  9 |    5 | 英语 |
|  5 | 陈四   |  26 |      0 | 10 |    5 | 数学 |
|  8 | 王语嫣 |  18 |      1 |  4 |    8 | 数学 |
|  8 | 王语嫣 |  18 |      1 |  5 |    8 | 历史 |
|  8 | 王语嫣 |  18 |      1 |  6 |    8 | 政治 |
+----+--------+-----+--------+----+------+------+
12 rows in set (0.01 sec)

mysql> select * from suser su LEFT JOIN course co ON su.id = co.s_id;
+----+--------+-----+--------+------+------+------+
| id | name   | age | gender | id   | s_id | name |
+----+--------+-----+--------+------+------+------+
|  1 | 陈波   |  26 |      0 |    1 |    1 | 数学 |
|  1 | 陈波   |  26 |      0 |    2 |    1 | 语文 |
|  1 | 陈波   |  26 |      0 |    3 |    1 | 英语 |
|  2 | 陈一   |  12 |      1 |    7 |    2 | 数学 |
|  2 | 陈一   |  12 |      1 |   11 |    2 | 历史 |
|  3 | 陈二   |  15 |      1 |    8 |    3 | 语文 |
|  4 | 陈三   |  32 |      0 |   12 |    4 | 政治 |
|  5 | 陈四   |  26 |      0 |    9 |    5 | 英语 |
|  5 | 陈四   |  26 |      0 |   10 |    5 | 数学 |
|  6 | 王一   |  26 |      0 | NULL | NULL | NULL |
|  7 | 王二   |  57 |      0 | NULL | NULL | NULL |
|  8 | 王语嫣 |  18 |      1 |    4 |    8 | 数学 |
|  8 | 王语嫣 |  18 |      1 |    5 |    8 | 历史 |
|  8 | 王语嫣 |  18 |      1 |    6 |    8 | 政治 |
|  9 | 陈嫣玉 |   0 |      1 | NULL | NULL | NULL |
| 10 |        |  40 |      1 | NULL | NULL | NULL |
+----+--------+-----+--------+------+------+------+
16 rows in set (0.00 sec)

mysql> select * from suser su RIGHT JOIN course co ON su.id = co.s_id;
+------+--------+------+--------+----+------+------+
| id   | name   | age  | gender | id | s_id | name |
+------+--------+------+--------+----+------+------+
|    1 | 陈波   |   26 |      0 |  1 |    1 | 数学 |
|    1 | 陈波   |   26 |      0 |  2 |    1 | 语文 |
|    1 | 陈波   |   26 |      0 |  3 |    1 | 英语 |
|    8 | 王语嫣 |   18 |      1 |  4 |    8 | 数学 |
|    8 | 王语嫣 |   18 |      1 |  5 |    8 | 历史 |
|    8 | 王语嫣 |   18 |      1 |  6 |    8 | 政治 |
|    2 | 陈一   |   12 |      1 |  7 |    2 | 数学 |
|    3 | 陈二   |   15 |      1 |  8 |    3 | 语文 |
|    5 | 陈四   |   26 |      0 |  9 |    5 | 英语 |
|    5 | 陈四   |   26 |      0 | 10 |    5 | 数学 |
|    2 | 陈一   |   12 |      1 | 11 |    2 | 历史 |
|    4 | 陈三   |   32 |      0 | 12 |    4 | 政治 |
+------+--------+------+--------+----+------+------+
12 rows in set (0.00 sec)
```
###### 排序
###### ASC
###### DESC
--排序
一般格式：
SELECT column,... FROM table WHERE 条件 ORDER BY column1,column2,... ASC | DESC;
默认升序排序。

SELECT * FROM t_user as t ORDER BY t.age asc ,t.count desc;
order by 多个字段时，用逗号分隔每一个字段，如果字段不指明排序方式，默认是增序。
排序的方法是首先按照第一个字段排序，如果第一个字段相同的，再按照第二个字段来再次排序，
从而产生排序结果。
###### 分组

--分组

    SELECT column_name, aggregate_function(column_name)
    FROM table_name
    WHERE column_name operator value
    GROUP BY column_name
    HAVING aggregate_function(column_name) operator value;
```
mysql> select * from score;
+----+------+--------+--------+------+
| id | s_id | s_name | c_name | num  |
+----+------+--------+--------+------+
|  1 |    1 | 陈波   | 数学   | 90.0 |
|  2 |    1 | 陈波   | 语文   | 87.5 |
|  3 |    1 | 陈波   | 英语   | 66.5 |
|  4 |    8 | 王语嫣 | 历史   | 80.0 |
+----+------+--------+--------+------+
```
分组会把重复数据过滤掉只显示第一条
```
mysql> select s_name,num from score group by s_id;
+--------+------+
| s_name | num  |
+--------+------+
| 陈波   | 90.0 |
| 王语嫣 | 80.0 |
+--------+------+
2 rows in set (0.00 sec)

mysql> select id,s_name 姓名,AVG(num) 平均分 from score group by s_id;
+----+--------+----------+
| id | 姓名   | 平均分   |
+----+--------+----------+
|  1 | 陈波   | 81.33333 |
|  4 | 王语嫣 | 80.00000 |
+----+--------+----------+
2 rows in set (0.01 sec)
```
计算每一组的数量
```
mysql> select id,s_name 姓名,AVG(num) 平均分,COUNT(*) 课程数量 from score group by s_id;
+----+--------+----------+----------+
| id | 姓名   | 平均分   | 课程数量 |
+----+--------+----------+----------+
|  1 | 陈波   | 81.33333 |        3 |
|  4 | 王语嫣 | 80.00000 |        1 |
+----+--------+----------+----------+
2 rows in set (0.00 sec)
```
HAVING条件的使用
```
mysql> select id,s_name 姓名,AVG(num) 平均分,COUNT(*) 课程数量 from score group by s_id HAVING 平均分>=80;
+----+--------+----------+----------+
| id | 姓名   | 平均分   | 课程数量 |
+----+--------+----------+----------+
|  1 | 陈波   | 81.33333 |        3 |
|  4 | 王语嫣 | 80.00000 |        1 |
+----+--------+----------+----------+
2 rows in set (0.01 sec)

mysql> select id,s_name 姓名,AVG(num) 平均分,COUNT(*) 课程数量 from score group by s_id HAVING 平均分>80;
+----+------+----------+----------+
| id | 姓名 | 平均分   | 课程数量 |
+----+------+----------+----------+
|  1 | 陈波 | 81.33333 |        3 |
+----+------+----------+----------+
1 row in set (0.00 sec)

mysql> select id,s_name 姓名,AVG(num) 平均分,COUNT(*) 课程数量 from score group by s_id HAVING AVG(num)>80;
+----+------+----------+----------+
| id | 姓名 | 平均分   | 课程数量 |
+----+------+----------+----------+
|  1 | 陈波 | 81.33333 |        3 |
+----+------+----------+----------+
1 row in set (0.00 sec)

mysql> select id,s_name 姓名,AVG(num) 平均分,COUNT(*) 课程数量 from score group by s_id HAVING s_name='陈波';
+----+------+----------+----------+
| id | 姓名 | 平均分   | 课程数量 |
+----+------+----------+----------+
|  1 | 陈波 | 81.33333 |        3 |
+----+------+----------+----------+
1 row in set (0.00 sec)

mysql> select id,s_name 姓名,AVG(num) 平均分,COUNT(*) 课程数量 from score group by s_id HAVING s_name='王语嫣';
+----+--------+----------+----------+
| id | 姓名   | 平均分   | 课程数量 |
+----+--------+----------+----------+
|  4 | 王语嫣 | 80.00000 |        1 |
+----+--------+----------+----------+
1 row in set (0.00 sec)
```
### 视图
### 索引
--创建索引
什么是索引？
索引便于快速检索数据，就是单独维护一份数据，这个数据有特殊的数据结构便于快速查询。
MySQL中只有ENGINE=InnoDB引擎才能创建索引。
1.主键索引:既有完整性约束，还有建立了索引
2.唯一索引
3.复合索引:既多个列组成的索引。
4.普通索引
创建索引的方式：
1.在创建表时创建：
CREATE TABLE `city` (
  `ID` int(11) NOT NULL AUTO_INCREMENT,
  `Name` char(35) NOT NULL DEFAULT '',
  `CountryCode` char(3) NOT NULL DEFAULT '',
  `District` char(20) NOT NULL DEFAULT '',
  `Population` int(11) NOT NULL DEFAULT '0',
  PRIMARY KEY (`ID`),//创建主键约束，并自动创建主键索引
  KEY `CountryCode` (`CountryCode`),//创建普通索引
  INDEX [indexName] (username(length)),//也是创建索引
  CONSTRAINT `city_ibfk_1` FOREIGN KEY (`CountryCode`) REFERENCES `country` (`code`)//创建外键约束
) ENGINE=InnoDB AUTO_INCREMENT=4080 DEFAULT CHARSET=latin1;

查看索引语句：
```
mysql> show index from course;\g
+--------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table  | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+--------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| course |          0 | PRIMARY  |            1 | id          | A         |          12 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| course |          0 | id       |            1 | id          | A         |          12 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| course |          1 | s_id     |            1 | s_id        | A         |           6 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
+--------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
3 rows in set (0.08 sec)

ERROR:
No query specified
```
查看表结构，查看索引类型，pri，mul.....
mysql> desc course;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| s_id  | int(11)     | NO   | MUL | NULL    |                |
| name  | varchar(20) | NO   |     |         |                |
+-------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)

2.直接创建索引：
CREATE INDEX index_name ON table_name(column1,column2,...);
3.修改表时创建索引：
ALTER table table_name ADD INDEX index_name(column1,column2,...);
ALTER table table_name ADD KEY index_name(column1,column2,...);
4.创建全文索引：
ALTER table table_name ADD FULLTEXT index_name(column1,column2,...);

删除索引：
DROP INDEX [indexName] ON table_name;
### 函数
### 权限控制


#### 更新
--UPDATE
鉴于以前出现的数据大表误更新和全表误删除操作。影响服务使用和数据安全。

为了防止线上业务出现以下3种情况影响线上服务的正常使用和不小心全表数据删除: 
1:没有加where条件的全表更新操作 ; 
2:加了where 条件字段，但是where 字段 没有走索引的表更新 ; 
3:全表delete 没有加where 条件 或者where 条件没有 走索引。 

语法的设置，管理员进入MySQL 
分global 和当前会话2种不同的 设置方式。 
set global sql_safe_updates = 1 | 0 ; //全局生效 ，1开启，0关闭
set sql_safe_updates = 1 | 0 ; //当前会话生效

一般格式：
UPDATE table_name SET column1=value1,column2=value2,... WHERE some_column=some_value;

请注意 SQL UPDATE 语句中的 WHERE 子句！
WHERE 子句规定哪条记录或者哪些记录需要更新。如果您省略了 WHERE 子句，所有的记录都将被更新！

--修改王语嫣的历史成绩为80分
```
UPDATE score SET num=80 WHERE s_name='王语嫣';
mysql> select * from score;
+----+------+--------+--------+------+
| id | s_id | s_name | c_name | num  |
+----+------+--------+--------+------+
|  1 |    1 | 陈波   | 数学   | 90.0 |
|  2 |    1 | 陈波   | 语文   | 87.5 |
|  3 |    1 | 陈波   | 英语   | 66.5 |
|  4 |    8 | 王语嫣 | 历史   | 80.0 |
+----+------+--------+--------+------+
4 rows in set (0.00 sec)
```
#### 删除

删除表数据
一般格式：
DELETE FROM table_name WHERE ...;

truncate table 命令将快速删除数据表中的所有记录，但保留数据表结构。这种快速删除与 delete from 数据表的删除全部数据表记录不一样，delete 命令删除的数据将存储在系统回滚段中，
需要的时候，数据可以回滚恢复，而 truncate 命令删除的数据是不可以恢复的。

相同点
truncate 和不带 where 子句的 delete, 以及 drop 都会删除表内的数据。

不同点:
1. truncate 和 delete 只删除数据不删除表的结构(定义) ，drop 语句将删除表的结构被依赖的约束(constrain), 触发器(trigger), 索引(index); 依赖于该表的存储过程/函数将保留,
 但是变为 invalid 状态。
2.delete 语句是 dml, 这个操作会放到 rollback segement 中, 事务提交之后才生效; 如果有相应的 trigger, 执行的时候将被触发。 truncate, drop 是 ddl, 操作立即生效, 
原数据不放到 rollback segment 中, 不能回滚。 操作不触发 trigger。
3.delete 语句不影响表所占用的 extent, 高水线(high watermark)保持原位置不动。 显然 drop 语句将表所占用的空间全部释放 。 
truncate 语句缺省情况下见空间释放到 minextents 个 extent, 除非使用 reuse storage; truncate会将高水线复位(回到最开始)。
4.速度：一般来说: drop > truncate > delete 。
5.安全性: 小心使用 drop 和 truncate, 尤其没有备份的时候。否则哭都来不及。

使用上, 想删除部分数据行用 delete, 注意带上 where 子句。 回滚段要足够大。
想删除表, 当然用 drop。
想保留表而将所有数据删除。如果和事务无关, 用 truncate 即可。 如果和事务有关, 或者想触发 trigger, 还是用 delete。
如果是整理表内部的碎片, 可以用 truncate 跟上 reuse stroage, 再重新导入/插入数据。
```
CREATE TABLE IF NOT EXISTS `custom`(
   `id` int not null UNIQUE AUTO_INCREMENT,
   `name` varchar(20) not null,
   primary KEY (`id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO custom VALUES (0,"王曦之"),(0,"刘怡"),(0,"张敏");
delete from custom where name='王曦之';//删除姓名='王曦之'的行
delete from custom;//删除表中全部数据
```
--删除数据
```
mysql> truncate custom;
Query OK, 0 rows affected (0.13 sec)
```
--删除表结构及数据
```
mysql> drop  table custom;
Query OK, 0 rows affected (0.13 sec)

mysql> show tables;
Empty set (0.01 sec)
```

#### 修改表结构
ALTER用法：
可以修改表和数据库的结构信息,包括：数据库，表字段，数据类型，索引等。

1.添加字段
```
ALTER TABLE custom ADD phoneNum int(11);

UPDATE custom set phoneNum=18288495581 where name="王曦之";
UPDATE custom set phoneNum=13934481267 where name="刘怡";
UPDATE custom set phoneNum=11111111111 where name="张敏";
```
发现phoneNum数据超出数据范围，修改表字段数据类型.
2.修改表字段数据类型
方式一：
```
alter table custom modify phoneNum char(11);
```
方式二：
在 CHANGE 关键字之后，紧跟着的是你要修改的字段名，然后指定新字段名及类型.
```
alter table custom change phoneNum phoneNum char(11);
```
重新插入数据：

```
UPDATE custom set phoneNum='18288495581' where name="王曦之";
UPDATE custom set phoneNum='13934481267' where name="刘怡";
UPDATE custom set phoneNum='11111111111' where name="张敏";
```
报错：
```
mysql> UPDATE custom set phoneNum='18288495581' where name="王曦之";
ERROR 1175 (HY000): You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column.
```
意思：where条件的column不是key，key会自动建立索引。

解决办法：建立索引。
1.方式一：
```
mysql> alter table custom add index `name` (`name`);
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc custom;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| id       | int(11)     | NO   | PRI | NULL    | auto_increment |
| name     | varchar(20) | NO   | MUL | NULL    |                |
| phoneNum | char(11)    | YES  |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```
2.方式二：
先把之前建立的索引删掉：
```
alter table custom drop index `name`;
```
重新创建索引：
```
mysql> alter table custom add key `name` (`name`);
Query OK, 0 rows affected (0.14 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc custom;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| id       | int(11)     | NO   | PRI | NULL    | auto_increment |
| name     | varchar(20) | NO   | MUL | NULL    |                |
| phoneNum | char(11)    | YES  |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```
修改字段默认值
```
mysql> desc custom;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| id       | int(11)     | NO   | PRI | NULL    | auto_increment |
| name     | varchar(20) | NO   | MUL | NULL    |                |
| phoneNum | char(11)    | YES  |     | NULL    |                |
| age      | int(3)      | YES  |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+

mysql> alter table custom alter age set default 0;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc custom;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| id       | int(11)     | NO   | PRI | NULL    | auto_increment |
| name     | varchar(20) | NO   | MUL | NULL    |                |
| phoneNum | char(11)    | YES  |     | NULL    |                |
| age      | int(3)      | YES  |     | 0       |                |
+----------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
```
删除默认值
```
mysql> alter table custom alter age drop default;
Query OK, 0 rows affected (0.08 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc custom;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| id       | int(11)     | NO   | PRI | NULL    | auto_increment |
| name     | varchar(20) | NO   | MUL | NULL    |                |
| phoneNum | char(11)    | YES  |     | NULL    |                |
| age      | int(3)      | YES  |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
```
修改表的引擎
```
ALTER TABLE testalter_tbl ENGINE = MYISAM;
```
查看表状态
```
mysql> SHOW TABLE STATUS LIKE 'custom' \G;\\\G格式化
*************************** 1. row ***************************
           Name: custom
         Engine: InnoDB
        Version: 10
     Row_format: Dynamic
           Rows: 3
 Avg_row_length: 5461
    Data_length: 16384
Max_data_length: 0
   Index_length: 32768
      Data_free: 0
 Auto_increment: 4
    Create_time: 2019-01-14 11:28:34
    Update_time: NULL
     Check_time: NULL
      Collation: utf8_general_ci
       Checksum: NULL
 Create_options:
        Comment:
1 row in set (0.10 sec)

ERROR:
No query specified

修改表名
mysql> ALTER TABLE custom RENAME TO custom2;
Query OK, 0 rows affected (0.06 sec)

mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| custom2        |
+----------------+
1 row in set (0.00 sec)
```

### CHEC约束
建表时，CHECK约束用于限制列中的值的范围。
```
CREATE TABLE IF NOT EXISTS `product`(
   `id` int not null UNIQUE auto_increment,
   `name` varchar(255) not null,
   `t_id` int,
   `t_name` varchar(255) comment `产品名称`,
   primary key (`id`),
   check (t_id > 0)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO product value (1,'手机',0,'电子产品');
mysql> INSERT INTO product value (1,'手机',0,'电子产品');
Query OK, 1 row affected (0.06 sec)
```
mysql中check约束无效。
解决这个问题的办法有两种方式：
1.如果设置CHECK约束字段范围小，并且比较容易列举全部的值，可以考虑把改字段的数据类型设置为enum()或集合类型set().
比如：假如这里的产品种类只有4种，可以把t_id字段设置为enum.
```
CREATE TABLE IF NOT EXISTS `product`(
   `id` int not null UNIQUE auto_increment,
   `name` varchar(255) not null,
   `t_id` enum('电子产品','化妆品','床上用品','食物') comment '产品id,1:电子产品，2：食物，3：生活用品，4：床上用品',
   `t_name` varchar(255) comment '产品名称',
   primary key (`id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
enum中必须是字符，不能是int.

2.如果需要设置的CHECK约束的字段范围很大，无法全部枚举，只能用触发器来代替check约束。
```
DELIMITER $
CREATE trigger t_id_check before insert on product for each row
begin
if new.t_id<1 then set
end if;
end $
DELIMITER;
```

### 触发器
-- 触发器是与表有关的数据库对象，在满足定义条件时触发，并执行触发器中定义的语句集合。触发器的这种特性可以协助应用在数据库端确保数据的完整性。
-- 创建触发器
```
CREATE TRIGGER trigger_name trigger_time trigger_event ON tb_name FOR EACH ROW trigger_stmt;
```
trigger_name：触发器的名称
tirgger_time：触发时机，为BEFORE或者AFTER
trigger_event：触发事件，为INSERT、DELETE或者UPDATE
tb_name：表示建立触发器的表明，就是在哪张表上建立触发器
trigger_stmt：触发器的程序体，可以是一条SQL语句或者是用BEGIN和END包含的多条语句

BEFORE和AFTER参数指定了触发执行的时间，在事件之前或是之后
FOR EACH ROW表示任何一条记录上的操作满足触发事件都会触发该触发器

--创建有多个执行语句的触发器
CREATE TRIGGER 触发器名 BEFORE|AFTER 触发事件
ON 表名 FOR EACH ROW
BEGIN
    执行语句列表
END
其中，BEGIN与END之间的执行语句列表参数表示需要执行的多个语句，不同语句用分号隔开。

tips：一般情况下，mysql默认是以 ; 作为结束执行语句，与触发器中需要的分行起冲突
　　   为解决此问题可用DELIMITER，如：DELIMITER ||，可以将结束符号变成||
　　   当触发器创建完成后，可以用DELIMITER ;来将结束符号变成;
```
mysql> DELIMITER ||
mysql> CREATE TRIGGER demo BEFORE DELETE
    -> ON users FOR EACH ROW
    -> BEGIN
    -> INSERT INTO logs VALUES(NOW());
    -> INSERT INTO logs VALUES(NOW());
    -> END
    -> ||
Query OK, 0 rows affected (0.06 sec)

mysql> DELIMITER ;
```

### 存储过程
使用到再学

