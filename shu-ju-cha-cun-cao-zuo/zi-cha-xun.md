# 子查询

子查询指一个查询语句嵌套在另一个查询语句内部的查询，这个特性从 MySQL 4.1 开始引入，在 SELECT 子句中先计算子查询，子查询结果作为外层另一个查询的过滤条件，查询可以基于一个表或者多个表。

 子查询中常用的操作符有 ANY（SOME）、ALL、IN 和 EXISTS。

 子查询可以添加到 SELECT、UPDATE 和 DELETE 语句中，而且可以进行多层嵌套。子查询也可以使用比较运算符，如“&lt;”、“&lt;=”、“&gt;”、“&gt;=”、“!=”等。

##  子查询中常用的运算符

###  1\) IN子查询

 结合关键字 IN 所使用的子查询主要用于判断一个给定值是否存在于子查询的结果集中。其语法格式为：

```text
<表达式> [NOT] IN <子查询>
```

 语法说明如下。

*  `<表达式>`：用于指定表达式。当表达式与子查询返回的结果集中的某个值相等时，返回 TRUE，否则返回 FALSE；若使用关键字 NOT，则返回的值正好相反。
*  `<子查询>`：用于指定子查询。这里的子查询只能返回一列数据。对于比较复杂的查询要求，可以使用 SELECT 语句实现子查询的多层嵌套。

###  2\) 比较运算符子查询

 比较运算符所使用的子查询主要用于对表达式的值和子查询返回的值进行比较运算。其语法格式为：

```text
<表达式> {= | < | > | >= | <= | <=> | < > | != } { ALL | SOME | ANY} <子查询>
```

 语法说明如下。

*  `<子查询>`：用于指定子查询。
*  `<表达式>`：用于指定要进行比较的表达式。
*  `ALL`、`SOME` 和 `ANY`：可选项。用于指定对比较运算的限制。其中，关键字 ALL 用于指定表达式需要与子查询结果集中的每个值都进行比较，当表达式与每个值都满足比较关系时，会返回 TRUE，否则返回 FALSE；关键字 SOME 和 ANY 是同义词，表示表达式只要与子查询结果集中的某个值满足比较关系，就返回 TRUE，否则返回 FALSE。

###  3\) EXIST子查询

 关键字 EXIST 所使用的子查询主要用于判断子查询的结果集是否为空。其语法格式为：

```text
 EXIST <子查询>
```

 若子查询的结果集不为空，则返回 TRUE；否则返回 FALSE。

##  子查询的应用

 【实例 1】在 tb\_departments 表中查询 dept\_type 为 A 的学院 ID，并根据学院 ID 查询该学院学生的名字，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT name FROM tb_students_info
    -> WHERE dept_id IN
    -> (SELECT dept_id
    -> FROM tb_departments
    -> WHERE dept_type= 'A' );
+-------+
| name  |
+-------+
| Dany  |
| Henry |
| Jane  |
| Jim   |
| John  |
+-------+
5 rows in set (0.01 sec)
```

 上述查询过程可以分步执行，首先内层子查询查出 tb\_departments 表中符合条件的学院 ID，单独执行内查询，查询结果如下所示。

```text
mysql> SELECT dept_id
    -> FROM tb_departments
    -> WHERE dept_type='A';
+---------+
| dept_id |
+---------+
|       1 |
|       2 |
+---------+
2 rows in set (0.00 sec)
```

 可以看到，符合条件的 dept\_id 列的值有两个：1 和 2。然后执行外层查询，在 tb\_students\_info 表中查询 dept\_id 等于 1 或 2 的学生的名字。嵌套子查询语句还可以写为如下形式，可以实现相同的效果。

```text
mysql> SELECT name FROM tb_students_info
    -> WHERE dept_id IN(1,2);
+-------+
| name  |
+-------+
| Dany  |
| Henry |
| Jane  |
| Jim   |
| John  |
+-------+
5 rows in set (0.03 sec)
```

 上例说明在处理 SELECT 语句时，MySQL 实际上执行了两个操作过程，即先执行内层子查询，再执行外层查询，内层子查询的结果作为外部查询的比较条件。

 【实例 2】与前一个例子类似，但是在 SELECT 语句中使用 NOT IN 关键字，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT name FROM tb_students_info
    -> WHERE dept_id NOT IN
    -> (SELECT dept_id
    -> FROM tb_departments
    -> WHERE dept_type='A');
+--------+
| name   |
+--------+
| Green  |
| Lily   |
| Susan  |
| Thomas |
| Tom    |
+--------+
5 rows in set (0.04 sec)
```

> 提示：子查询的功能也可以通过连接查询完成，但是子查询使得 MySQL 代码更容易阅读和编写。

 【实例 3】在 tb\_departments 表中查询 dept\_name 等于“Computer”的学院 id，然后在 tb\_students\_info 表中查询所有该学院的学生的姓名，输入的 SQL 语句和执行过程如下所示。

```text
 mysql> SELECT name FROM tb_students_info
    -> WHERE dept_id =
    -> (SELECT dept_id
    -> FROM tb_departments
    -> WHERE dept_name='Computer');
+------+
| name |
+------+
| Dany |
| Jane |
| Jim  |
+------+
3 rows in set (0.00 sec)
```

 【实例 4】在 tb\_departments 表中查询 dept\_name 不等于“Computer”的学院 id，然后在 tb\_students\_info 表中查询所有该学院的学生的姓名，输入的 SQL 语句和执行过程如下所示。

```text
mysql> SELECT name FROM tb_students_info
    -> WHERE dept_id <>
    -> (SELECT dept_id
    -> FROM tb_departments
    -> WHERE dept_name='Computer');
+--------+
| name   |
+--------+
| Green  |
| Henry  |
| John   |
| Lily   |
| Susan  |
| Thomas |
| Tom    |
+--------+
7 rows in set (0.00 sec)
```

 【实例 5】查询 tb\_departments 表中是否存在 dept\_id=1 的供应商，如果存在，就查询 tb\_students\_info 表中的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_students_info
    -> WHERE EXISTS
    -> (SELECT dept_name
    -> FROM tb_departments
    -> WHERE dept_id=1);
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

 由结果可以看到，内层查询结果表明 tb\_departments 表中存在 dept\_id=1 的记录，因此 EXSTS 表达式返回 TRUE，外层查询语句接收 TRUE 之后对表 tb\_students\_info 进行查询，返回所有的记录。

 EXISTS 关键字可以和条件表达式一起使用。

 【实例 6】查询 tb\_departments 表中是否存在 dept\_id=7 的供应商，如果存在，就查询 tb\_students\_info 表中的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_students_info
    -> WHERE EXISTS
    -> (SELECT dept_name
    -> FROM tb_departments
    -> WHERE dept_id=7);
Empty set (0.00 sec)
```

