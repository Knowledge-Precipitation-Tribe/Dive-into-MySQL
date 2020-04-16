# 内连接查询

在 MySQL FROM 子句中使用关键字 INNER JOIN 连接两张表，并使用ON子句来设置连接条件。如果没有任何条件，INNER JOIN和CROSS JOIN在语法上是等同的，两者可以互换。

 语法格式如下：

```text
SELECT <列名1，列名2 …> FROM <表名1> INNER JOIN <表名2> [ ON子句]
```

语法说明如下。

*  `<列名1，列名2…>`：需要检索的列名。
*  `<表名1><表名2>`：进行内连接的两张表的表名。

内连接是系统默认的表连接，所以在 FROM 子句后可以省略 INNER 关键字，只用关键字 JOIN。使用内连接后，FROM 子句中的 ON 子句可用来设置连接表的条件。

在 FROM 子句中可以在多个表之间连续使用 INNER JOIN 或 JOIN，如此可以同时实现多个表的内连接。

表 tb\_students\_info 和表 tb\_departments 都包含相同数据类型的字段 dept\_id，在两个表之间使用内连接查询。输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT id,name,age,dept_name
    -> FROM tb_students_info,tb_departments
    -> WHERE tb_students_info.dept_id=tb_departments.dept_id;
+----+--------+------+-----------+
| id | name   | age  | dept_name |
+----+--------+------+-----------+
|  1 | Dany   |   25 | Computer  |
|  2 | Green  |   23 | Chinese   |
|  3 | Henry  |   23 | Math      |
|  4 | Jane   |   22 | Computer  |
|  5 | Jim    |   24 | Computer  |
|  6 | John   |   21 | Math      |
|  7 | Lily   |   22 | Computer  |
|  8 | Susan  |   23 | Economy   |
|  9 | Thomas |   22 | Chinese   |
| 10 | Tom    |   23 | Economy   |
+----+--------+------+-----------+
10 rows in set (0.00 sec)
```

在这里，SELECT 语句与前面介绍的最大差别是：SELECT 后面指定的列分别属于两个不同的表，id、name、age 在表 tb\_students\_info 中，而 dept\_name 在表 tb\_departments 中，同时 FROM 字句列出了两个表 tb\_students\_info 和 tb\_departments。WHERE 子句在这里作为过滤条件，指明只有两个表中的 dept\_id 字段值相等的时候才符合连接查询的条件。

 返回的结果可以看到，显示的记录是由两个表中的不同列值组成的新记录。

> 提示：因为 tb\_students\_info 表和 tb\_departments 表中有相同的字段 dept\_id，所以在比较的时候，需要完全限定表名（格式为“表名.列名”），如果只给出 dept\_id，MySQL 将不知道指的是哪一个，并返回错误信息。

在 tb\_students\_info 表和 tb\_departments 表之间，使用 INNER JOIN 语法进行内连接查询，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT id,name,age,dept_name
    -> FROM tb_students_info INNER JOIN tb_departments
    -> ON tb_students_info.dept_id=tb_departments.dept_id;
+----+--------+------+-----------+
| id | name   | age  | dept_name |
+----+--------+------+-----------+
|  1 | Dany   |   25 | Computer  |
|  2 | Green  |   23 | Chinese   |
|  3 | Henry  |   23 | Math      |
|  4 | Jane   |   22 | Computer  |
|  5 | Jim    |   24 | Computer  |
|  6 | John   |   21 | Math      |
|  7 | Lily   |   22 | Computer  |
|  8 | Susan  |   23 | Economy   |
|  9 | Thomas |   22 | Chinese   |
| 10 | Tom    |   23 | Economy   |
+----+--------+------+-----------+
10 rows in set (0.00 sec)
```

在这里的查询语句中，两个表之间的关系通过 INNER JOIN 指定。使用这种语法的时候，连接的条件使用 ON 子句给出，而不是 WHERE，ON 和 WHERE 后面指定的条件相同。

> 提示：使用 WHERE 子句定义连接条件比较简单明了，而 INNER JOIN 语法是 ANSI SQL 的标准规范，使用 INNER JOIN 连接语法能够确保不会忘记连接条件，而且 WHERE 子句在某些时候会影响查询的性能。

