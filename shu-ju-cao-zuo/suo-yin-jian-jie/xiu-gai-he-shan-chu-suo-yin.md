# 修改和删除索引

在 MySQL 中修改索引可以通过删除原索引，再根据需要创建一个同名的索引，从而实现修改索引的操作。

##  基本语法

 当不再需要索引时，可以使用 DROP INDEX 语句或 ALTER TABLE 语句来对索引进行删除。

###  1\) 使用 DROP INDEX 语句

 语法格式：

```text
DROP INDEX <索引名> ON <表名>
```

 语法说明如下：

*  `<索引名>`：要删除的索引名。
*  `<表名>`：指定该索引所在的表名。

###  2\) 使用 ALTER TABLE 语句

 根据 ALTER TABLE 语句的语法可知，该语句也可以用于删除索引。具体使用方法是将 ALTER TABLE 语句的语法中部分指定为以下子句中的某一项。

*  DROP PRIMARY KEY：表示删除表中的主键。一个表只有一个主键，主键也是一个索引。
*  DROP INDEX index\_name：表示删除名称为 index\_name 的索引。
*  DROP FOREIGN KEY fk\_symbol：表示删除外键。

> 注意：如果删除的列是索引的组成部分，那么在删除该列时，也会将该列从索引中删除；如果组成索引的所有列都被删除，那么整个索引将被删除。

##  删除索引

 【实例 1】删除表 tb\_stu\_info 中的索引，输入的 SQL 语句和执行结果如下所示。

```sql
mysql> DROP INDEX height
    -> ON tb_stu_info;
Query OK, 0 rows affected (0.27 sec)
Records: 0  Duplicates: 0  Warnings: 0
mysql> SHOW CREATE TABLE tb_stu_info\G
*************************** 1. row ***************************
       Table: tb_stu_info
Create Table: CREATE TABLE `tb_stu_info` (
  `id` int(11) NOT NULL,
  `name` char(45) DEFAULT NULL,
  `dept_id` int(11) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `height` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=gb2312
1 row in set (0.00 sec)
```

 【实例 2】删除表 tb\_stu\_info2 中名称为 id 的索引，输入的 SQL 语句和执行结果如下所示。

```sql
mysql> ALTER TABLE tb_stu_info2
    -> DROP INDEX height;
Query OK, 0 rows affected (0.13 sec)
Records: 0  Duplicates: 0  Warnings: 0
mysql> SHOW CREATE TABLE tb_stu_info2\G
*************************** 1. row ***************************
       Table: tb_stu_info2
Create Table: CREATE TABLE `tb_stu_info2` (
  `id` int(11) NOT NULL,
  `name` char(45) DEFAULT NULL,
  `dept_id` int(11) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `height` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=gb2312
1 row in set (0.00 sec)
```

