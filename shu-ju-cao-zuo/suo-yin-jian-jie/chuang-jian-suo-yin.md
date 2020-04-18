# 创建索引

索引的建立对于 MySQL 数据库的高效运行是很重要的，索引可以大大提升 MySQL 的检索速度。

##  基本语法

 MySQL 提供了三种创建索引的方法：

###  1\) 使用 CREATE INDEX 语句

 可以使用专门用于创建索引的 CREATE INDEX 语句在一个已有的表上创建索引，但该语句不能创建主键。

 语法格式：

```text
CREATE <索引名> ON <表名> (<列名> [<长度>] [ ASC | DESC])
```

 语法说明如下：

*  `<索引名>`：指定索引名。一个表可以创建多个索引，但每个索引在该表中的名称是唯一的。
*  `<表名>`：指定要创建索引的表名。
*  `<列名>`：指定要创建索引的列名。通常可以考虑将查询语句中在 JOIN 子句和 WHERE 子句里经常出现的列作为索引列。
*  `<长度>`：可选项。指定使用列前的 length 个字符来创建索引。使用列的一部分创建索引有利于减小索引文件的大小，节省索引列所占的空间。在某些情况下，只能对列的前缀进行索引。索引列的长度有一个最大上限 255 个字节（MyISAM 和 InnoDB 表的最大上限为 1000 个字节），如果索引列的长度超过了这个上限，就只能用列的前缀进行索引。另外，BLOB 或 TEXT 类型的列也必须使用前缀索引。
*  `ASC|DESC`：可选项。`ASC`指定索引按照升序来排列，`DESC`指定索引按照降序来排列，默认为`ASC`。

###  2\) 使用 CREATE TABLE 语句

 索引也可以在创建表（CREATE TABLE）的同时创建。在 CREATE TABLE 语句中添加以下语句。语法格式：

```text
CONSTRAINT PRIMARY KEY [索引类型] (<列名>,…)
```

 在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的主键。

 语法格式：

```text
KEY | INDEX [<索引名>] [<索引类型>] (<列名>,…)
```

 在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的索引。

 语法格式：

```text
UNIQUE [ INDEX | KEY] [<索引名>] [<索引类型>] (<列名>,…)
```

 在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的唯一性索引。

 语法格式：

```text
FOREIGN KEY <索引名> <列名>
```

 在 CREATE TABLE 语句中添加此语句，表示在创建新表的同时创建该表的外键。

 在使用 CREATE TABLE 语句定义列选项的时候，可以通过直接在某个列定义后面添加 PRIMARY KEY 的方式创建主键。而当主键是由多个列组成的多列索引时，则不能使用这种方法，只能用在语句的最后加上一个 PRIMARY KRY\(&lt;列名&gt;，…\) 子句的方式来实现。

###  3\) 使用 ALTER TABLE 语句

 CREATE INDEX 语句可以在一个已有的表上创建索引，ALTER TABLE 语句也可以在一个已有的表上创建索引。在使用 ALTER TABLE 语句修改表的同时，可以向已有的表添加索引。具体的做法是在 ALTER TABLE 语句中添加以下语法成分的某一项或几项。

 语法格式：

```text
ADD INDEX [<索引名>] [<索引类型>] (<列名>,…)
```

 在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加索引。

 语法格式：

```text
ADD PRIMARY KEY [<索引类型>] (<列名>,…)
```

 在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加主键。

 语法格式：

```text
ADD UNIQUE [ INDEX | KEY] [<索引名>] [<索引类型>] (<列名>,…)
```

 在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加唯一性索引。

 语法格式：

```text
ADD FOREIGN KEY [<索引名>] (<列名>,…)
```

 在 ALTER TABLE 语句中添加此语法成分，表示在修改表的同时为该表添加外键。

##  创建一般索引

 【实例 1】创建一个表 tb\_stu\_info，在该表的 height 字段创建一般索引。输入的 SQL 语句和执行过程如下所示。

```text
mysql> CREATE TABLE tb_stu_info
    -> (
    -> id INT NOT NULL,
    -> name CHAR(45) DEFAULT NULL,
    -> dept_id INT DEFAULT NULL,
    -> age INT DEFAULT NULL,
    -> height INT DEFAULT NULL,
    -> INDEX(height)
    -> );
Query OK，0 rows affected (0.40 sec)
mysql> SHOW CREATE TABLE tb_stu_info\G
*************************** 1. row ***************************
       Table: tb_stu_info
Create Table: CREATE TABLE `tb_stu_info` (
  `id` int(11) NOT NULL,
  `name` char(45) DEFAULT NULL,
  `dept_id` int(11) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `height` int(11) DEFAULT NULL,
  KEY `height` (`height`)
) ENGINE=InnoDB DEFAULT CHARSET=gb2312
1 row in set (0.01 sec)
```

##  创建唯一索引

 【实例 2】创建一个表 tb\_stu\_info2，在该表的 id 字段上使用 UNIQUE 关键字创建唯一索引。输入的 SQL 语句和执行过程如下所示。

```text
mysql> CREATE TABLE tb_stu_info2
    -> (
    -> id INT NOT NULL,
    -> name CHAR(45) DEFAULT NULL,
    -> dept_id INT DEFAULT NULL,
    -> age INT DEFAULT NULL,
    -> height INT DEFAULT NULL,
    -> UNIQUE INDEX(height)
    -> );
Query OK，0 rows affected (0.40 sec)
mysql> SHOW CREATE TABLE tb_stu_info2\G
*************************** 1. row ***************************
       Table: tb_stu_info2
Create Table: CREATE TABLE `tb_stu_info2` (
  `id` int(11) NOT NULL,
  `name` char(45) DEFAULT NULL,
  `dept_id` int(11) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `height` int(11) DEFAULT NULL,
  UNIQUE KEY `height` (`height`)
) ENGINE=InnoDB DEFAULT CHARSET=gb2312
1 row in set (0.00 sec)
```

##  查看索引

 在 MySQL 中，如果要查看已创建的索引的情况，可以使用 SHOW INDEX 语句查看表中创建的索引。

 语法格式：

```text
SHOW INDEX FROM <表名> [ FROM <数据库名>]
```

 语法说明如下：

*  `<表名>`：要显示索引的表。
*  `<数据库名>`：要显示的表所在的数据库。

 显示数据库 mytest 的表 course 的索引情况。

```text
mysql> SHOW INDEX FROM course FROM mytest;
```

 该语句会返回一张结果表，该表有如下几个字段，每个字段所显示的内容说明如下。

*  Table：表的名称。
*  Non\_unique：用于显示该索引是否是唯一索引。若不是唯一索引，则该列的值显示为 1；若是唯一索引，则该列的值显示为 0。
*  Key\_name：索引的名称。
*  Seq\_in\_index：索引中的列序列号，从 1 开始计数。
*  Column\_name：列名称。
*  Collation：显示列以何种顺序存储在索引中。在 MySQL 中，升序显示值“A”（升序），若显示为 NULL，则表示无分类。
*  Cardinality：显示索引中唯一值数目的估计值。基数根据被存储为整数的统计数据计数，所以即使对于小型表，该值也没有必要是精确的。基数越大，当进行联合时，MySQL 使用该索引的机会就越大。
*  Sub\_part：若列只是被部分编入索引，则为被编入索引的字符的数目。若整列被编入索引，则为 NULL。
*  Packed：指示关键字如何被压缩。若没有被压缩，则为 NULL。
*  Null：用于显示索引列中是否包含 NULL。若列含有 NULL，则显示为 YES。若没有，则该列显示为 NO。
*  Index\_type：显示索引使用的类型和方法（BTREE、FULLTEXT、HASH、RTREE）。
*  Comment：显示评注。

 【实例 3】使用 SHOW INDEX 语句查看表 tb\_stu\_info2 的索引信息，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SHOW INDEX FROM tb_stu_info2\G
*************************** 1. row ***************************
        Table: tb_stu_info2
   Non_unique: 0
     Key_name: height
Seq_in_index: 1
  Column_name: height
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: YES
   Index_type: BTREE
      Comment:
Index_comment:
1 row in set (0.03 sec)
```

