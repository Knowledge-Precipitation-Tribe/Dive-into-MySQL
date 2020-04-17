# 删除视图

删除视图是指删除 MySQL 数据库中已存在的视图。删除视图时，只能删除视图的定义，不会删除数据。

##  基本语法

 可以使用 DROP VIEW 语句来删除视图。

 语法格式如下：

```text
DROP VIEW <视图名1> [ , <视图名2> …]
```

 其中：`<视图名>` 指定要删除的视图名。DROP VIEW 语句可以一次删除多个视图，但是必须在每个视图上拥有 DROP 权限。

##  删除视图

 【实例】删除 v\_students\_info 视图，输入的 SQL 语句和执行过程如下所示。

```text
mysql> DROP VIEW IF EXISTS v_students_info;
Query OK, 0 rows affected (0.00 sec)
mysql> SHOW CREATE VIEW v_students_info;
ERROR 1146 (42S02): Table 'test_db.v_students_info' doesn't exist
```

 可以看到，v\_students\_info 视图已不存在，将其成功删除。

