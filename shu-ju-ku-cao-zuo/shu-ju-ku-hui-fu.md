# 数据库恢复

数据库恢复是指以备份为基础，与备份相对应的系统维护和管理操作。

 系统进行恢复操作时，先执行一些系统安全性的检查，包括检查所要恢复的数据库是否存在、数据库是否变化及数据库文件是否兼容等，然后根据所采用的数据库备份类型采取相应的恢复措施。

 数据库恢复机制设计的两个关键问题是：第一，如何建立冗余数据；第二，如何利用这些冗余数据实施数据库恢复。

 建立冗余数据最常用的技术是数据转储和登录日志文件。通常在一个数据库系统中，这两种方法是一起使用的。

 数据转储是 DBA 定期地将整个数据库复制到磁带或另一个磁盘上保存起来的过程。这些备用的版本成为后备副本或后援副本。

 可使用 LOAD DATA…INFILE 语句来恢复先前备份的数据。

 【实例】将之前导出的数据备份文件 file.txt 导入数据库 test\_db 的表 tb\_students\_copy 中，其中 tb\_students\_copy 的表结构和 tb\_students\_info 相同。

 首先创建表 tb\_students\_copy，输入的 SQL 语句和执行结果如下所示。

```text
mysql> CREATE TABLE tb_students_copy
    -> LIKE tb_students_info;
Query OK, 0 rows affected (0.52 sec)
mysql> SELECT * FROM tb_students_copy;
Empty set (0.00 sec)
```

 导入数据与查询表 tb\_students\_copy 的过程如下所示。

```text
mysql> LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 5.7/
Uploads/file.txt'
    -> INTO TABLE test_db.tb_students_copy
    -> FIELDS TERMINATED BY ','
    -> OPTIONALLY ENCLOSED BY '"'
    -> LINES TERMINATED BY '?';
Query OK, 10 rows affected (0.14 sec)
Records: 10  Deleted: 0  Skipped: 0  Warnings: 0
mysql> SELECT * FROM test_db.tb_students_copy;
+----+--------+---------+------+------+--------+------------+
| id | name   | dept_id | age  | sex  | height | login_date |
+----+--------+---------+------+------+--------+------------+
|  1 | Dany   |       1 |   25 | F    |    160 | 2015-09-10 |
|  2 | Green  |       3 |   23 | F    |    158 | 2016-10-22 |
|  3 | Henry  |       2 |   23 | M    |    185 | 2015-05-31 |
|  4 | Jane   |       1 |   22 | F    |    162 | 2016-12-20 |
|  5 | Jim    |       1 |   24 | M    |    175 | 2016-01-15 |
|  6 | John   |       2 |   21 | M    |    172 | 2015-11-11 |
|  7 | Lily   |       6 |   22 | F    |    165 | 2016-02-26 |
|  8 | Susan  |       4 |   23 | F    |    170 | 2015-10-01 |
|  9 | Thomas |       3 |   22 | M    |    178 | 2016-06-07 |
| 10 | Tom    |       4 |   23 | M    |    165 | 2016-08-05 |
+----+--------+---------+------+------+--------+------------+
10 rows in set (0.00 sec)
```

