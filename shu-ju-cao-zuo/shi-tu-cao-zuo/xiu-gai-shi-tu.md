# 修改视图

修改视图是指修改 MySQL 数据库中存在的视图，当基本表的某些字段发生变化时，可以通过修改视图来保持与基本表的一致性。

##  基本语法

 可以使用 ALTER VIEW 语句来对已有的视图进行修改。

 语法格式如下：

```text
ALTER VIEW <视图名> AS <SELECT语句>
```

 语法说明如下：

*  `<视图名>`：指定视图的名称。该名称在数据库中必须是唯一的，不能与其他表或视图同名。
*  `<SELECT 语句>`：指定创建视图的 SELECT 语句，可用于查询多个基础表或源视图。

 需要注意的是，对于 ALTER VIEW 语句的使用，需要用户具有针对视图的 CREATE VIEW 和 DROP 权限，以及由 SELECT 语句选择的每一列上的某些权限。

 修改视图的定义，除了可以通过 ALTER VIEW 外，也可以使用 DROP VIEW 语句先删除视图，再使用 CREATE VIEW 语句来实现。

##  修改视图内容

 视图是一个虚拟表，实际的数据来自于基本表，所以通过插入、修改和删除操作更新视图中的数据，实质上是在更新视图所引用的基本表的数据。

{% hint style="danger" %}
对视图的修改就是对基本表的修改，因此在修改时，要满足基本表的数据定义。
{% endhint %}

 某些视图是可更新的。也就是说，可以使用 UPDATE、DELETE 或 INSERT 等语句更新基本表的内容。对于可更新的视图，视图中的行和基本表的行之间必须具有一对一的关系。

 还有一些特定的其他结构，这些结构会使得视图不可更新。更具体地讲，如果视图包含以下结构中的任何一种，它就是不可更新的：

*  聚合函数 SUM\(\)、MIN\(\)、MAX\(\)、COUNT\(\) 等。
*  DISTINCT 关键字。
*  GROUP BY 子句。
*  HAVING 子句。
*  UNION 或 UNION ALL 运算符。
*  位于选择列表中的子查询。
*  FROM 子句中的不可更新视图或包含多个表。
*  WHERE 子句中的子查询，引用 FROM 子句中的表。
*  ALGORITHM 选项为 TEMPTABLE（使用临时表总会使视图成为不可更新的）的时候。

 【实例 1】使用 ALTER 语句修改视图 view\_students\_info，输入的 SQL 语句和执行结果如下所示。

```text
mysql> ALTER VIEW view_students_info
    -> AS SELECT id,name,age
    -> FROM tb_students_info;
Query OK, 0 rows affected (0.07 sec)
mysql> DESC view_students_info;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   |     | 0       |       |
| name  | varchar(45) | YES  |     | NULL    |       |
| age   | int(11)     | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.03 sec)
```

 用户可以通过视图来插入、更新、删除表中的数据，因为视图是一个虚拟的表，没有数据。通过视图更新时转到基本表上进行更新，如果对视图增加或删除记录，实际上是对基本表增加或删除记录。

 查看视图 view\_students\_info 的数据内容，如下所示。

```text
mysql> SELECT * FROM view_students_info;
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Dany   |   24 |
|  2 | Green  |   23 |
|  3 | Henry  |   23 |
|  4 | Jane   |   22 |
|  5 | Jim    |   24 |
|  6 | John   |   21 |
|  7 | Lily   |   22 |
|  8 | Susan  |   23 |
|  9 | Thomas |   22 |
| 10 | Tom    |   23 |
+----+--------+------+
10 rows in set (0.00 sec)
```

 【实例 2】使用 UPDATE 语句更新视图 view\_students\_info，输入的 SQL 语句和执行结果如下所示。

```text
mysql> UPDATE view_students_info
    -> SET age=25 WHERE id=1;
Query OK, 0 rows affected (0.24 sec)
Rows matched: 1  Changed: 0  Warnings: 0
mysql> SELECT * FROM view_students_info;
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Dany   |   25 |
|  2 | Green  |   23 |
|  3 | Henry  |   23 |
|  4 | Jane   |   22 |
|  5 | Jim    |   24 |
|  6 | John   |   21 |
|  7 | Lily   |   22 |
|  8 | Susan  |   23 |
|  9 | Thomas |   22 |
| 10 | Tom    |   23 |
+----+--------+------+
10 rows in set (0.00 sec)
```

 查看基本表 tb\_students\_info 和视图 v\_students\_info 的内容，如下所示。

```text
mysql> SELECT * FROM tb_students_info;
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

mysql> SELECT * FROM v_students_info;
+------+--------+------+-------+-------+----------+------------+
| s_id | s_name | d_id | s_age | s_sex | s_height | s_date     |
+------+--------+------+-------+-------+----------+------------+
|    1 | Dany   |    1 |    25 | F     |      160 | 2015-09-10 |
|    2 | Green  |    3 |    23 | F     |      158 | 2016-10-22 |
|    3 | Henry  |    2 |    23 | M     |      185 | 2015-05-31 |
|    4 | Jane   |    1 |    22 | F     |      162 | 2016-12-20 |
|    5 | Jim    |    1 |    24 | M     |      175 | 2016-01-15 |
|    6 | John   |    2 |    21 | M     |      172 | 2015-11-11 |
|    7 | Lily   |    6 |    22 | F     |      165 | 2016-02-26 |
|    8 | Susan  |    4 |    23 | F     |      170 | 2015-10-01 |
|    9 | Thomas |    3 |    22 | M     |      178 | 2016-06-07 |
|   10 | Tom    |    4 |    23 | M     |      165 | 2016-08-05 |
+------+--------+------+-------+-------+----------+------------+
10 rows in set (0.00 sec)
```

##  修改视图名称

 修改视图的名称可以先将视图删除，然后按照相同的定义语句进行视图的创建，并命名为新的视图名称。

