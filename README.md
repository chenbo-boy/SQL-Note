# SQL-Note2 SQL语法学习
##### MySql-SQL语法
## 目录
+ [数据库(模式schema)](#数据库)
  + [查看所有数据库]
  + [查看指定数据库中的表]
  + [切换数据库]
+ [表操作](#表操作)
  + [数据类型]
  + [创建表](#创建表)
  + [插入数据](#插入数据)
  + [查询](#查询)
    + [查询表结构]
    + [查询建表语句]
    + [一般查询格式](#一般查询格式)
    + [ALL|DISTINCT]
    + [条件查询](#条件查询)
      + [比较运算符]
      + [确定范围]
        + [BETWEEN AND]
        + [NOT BETWEEN AND]
      + [确定集合]
        + [IN]
        + [NOT IN]
      + [字符匹配]
        + [LIKE]
        + [NOT LIKE]
        + [REGEXP | RLIKE]
        + [NOT REGEXP | NOT RLIKE]
      + [空值]
        + [IS NULL]
        + [IS NOT NULL]
      + [逻辑运算]
        + [AND]
        + [OR]
        + [NOT]
      + [UNION]
      + [UNION ALL]
      + [LIMIT]
      + [别名]
        + [CONCAT]
    + [嵌套查询]
    + [排序]
      + [ASC]
      + [DESC]
    + [分组]
+ 试图
+ 索引
+ 函数
+ 触发器
+ 权限控制

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
其实所有表和数据库的信息都在information_schema表里。
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
```


