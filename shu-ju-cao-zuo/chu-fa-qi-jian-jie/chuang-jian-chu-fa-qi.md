# 创建触发器

触发器是与 MySQL 数据表有关的数据库对象，在满足定义条件时触发，并执行触发器中定义的语句集合。触发器的这种特性可以协助应用在数据库端确保数据的完整性。

##  基本语法

 在 MySQL 5.7 中，可以使用 CREATE TRIGGER 语句创建触发器。

 语法格式如下：

```text
CREATE TRIGGER <触发器名> < BEFORE | AFTER > <INSERT | UPDATE | DELETE > ON <表名> FOR EACH Row<触发器主体>
```

 语法说明如下。

###  1\) 触发器名

 触发器的名称，触发器在当前数据库中必须具有唯一的名称。如果要在某个特定数据库中创建，名称前面应该加上数据库的名称。

###  2\) INSERT \| UPDATE \| DELETE

 触发事件，用于指定激活触发器的语句的种类。

 注意：三种触发器的执行时间如下。

*  INSERT：将新行插入表时激活触发器。例如，INSERT 的 BEFORE 触发器不仅能被 MySQL 的 INSERT 语句激活，也能被 LOAD DATA 语句激活。
*  DELETE： 从表中删除某一行数据时激活触发器，例如 DELETE 和 REPLACE 语句。
*  UPDATE：更改表中某一行数据时激活触发器，例如 UPDATE 语句。

###  3\) BEFORE \| AFTER

 BEFORE 和 AFTER，触发器被触发的时刻，表示触发器是在激活它的语句之前或之后触发。若希望验证新数据是否满足条件，则使用 BEFORE 选项；若希望在激活触发器的语句执行之后完成几个或更多的改变，则通常使用 AFTER 选项。

###  4\) 表名

 与触发器相关联的表名，此表必须是永久性表，不能将触发器与临时表或视图关联起来。在该表上触发事件发生时才会激活触发器。同一个表不能拥有两个具有相同触发时刻和事件的触发器。例如，对于一张数据表，不能同时有两个 BEFORE UPDATE 触发器，但可以有一个 BEFORE UPDATE 触发器和一个 BEFORE INSERT 触发器，或一个 BEFORE UPDATE 触发器和一个 AFTER UPDATE 触发器。

###  5\) 触发器主体

 触发器动作主体，包含触发器激活时将要执行的 MySQL 语句。如果要执行多个语句，可使用 BEGIN…END 复合语句结构。

###  6\) FOR EACH ROW

 一般是指行级触发，对于受触发事件影响的每一行都要激活触发器的动作。例如，使用 INSERT 语句向某个表中插入多行数据时，触发器会对每一行数据的插入都执行相应的触发器动作。

> 注意：每个表都支持 INSERT、UPDATE 和 DELETE 的 BEFORE 与 AFTER，因此每个表最多支持 6 个触发器。每个表的每个事件每次只允许有一个触发器。单一触发器不能与多个事件或多个表关联。

 另外，在 MySQL 中，若需要查看数据库中已有的触发器，则可以使用 SHOW TRIGGERS 语句。

## 创建 BEFORE 类型触发器

在 test\_db 数据库中，数据表 tb\_emp8 为员工信息表，包含 id、name、deptId 和 salary 字段，数据表 tb\_emp8 的表结构如下所示。

```text
mysql> SELECT * FROM tb_emp8;
Empty set (0.07 sec)
mysql> DESC tb_emp8;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int(11)     | NO   | PRI | NULL    |       |
| name   | varchar(22) | YES  | UNI | NULL    |       |
| deptId | int(11)     | NO   | MUL | NULL    |       |
| salary | float       | YES  |     | 0       |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.05 sec)
```

【实例 1】创建一个名为 SumOfSalary 的触发器，触发的条件是向数据表 tb\_emp8 中插入数据之前，对新插入的 salary 字段值进行求和计算。输入的 SQL 语句和执行过程如下所示。

```text
mysql> CREATE TRIGGER SumOfSalary
    -> BEFORE INSERT ON tb_emp8
    -> FOR EACH ROW
    -> SET @sum=@sum+NEW.salary;
Query OK, 0 rows affected (0.35 sec)
```

触发器 SumOfSalary 创建完成之后，向表 tb\_emp8 中插入记录时，定义的 sum 值由 0 变成了1500，即插入值 1000 和 500 的和，如下所示。

```text
mysql> SET @sum=0;
Query OK, 0 rows affected (0.05 sec)
mysql> INSERT INTO tb_emp8
    -> VALUES(1,'A',1,1000),(2,'B',1,500);
Query OK, 2 rows affected (0.09 sec)
Records: 2  Duplicates: 0  Warnings: 0
mysql> SELECT @sum;
+------+
| @sum |
+------+
| 1500 |
+------+
1 row in set (0.03 sec)
```

##  创建 AFTER 类型触发器

在 test\_db 数据库中，数据表 tb\_emp6 和 tb\_emp7 都为员工信息表，包含 id、name、deptId 和 salary 字段，数据表 tb\_emp6 和 tb\_emp7 的表结构如下所示。

```text
mysql> SELECT * FROM tb_emp6;
Empty set (0.07 sec)
mysql> SELECT * FROM tb_emp7;
Empty set (0.03 sec)
mysql> DESC tb_emp6;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int(11)     | NO   | PRI | NULL    |       |
| name   | varchar(25) | YES  |     | NULL    |       |
| deptId | int(11)     | YES  | MUL | NULL    |       |
| salary | float       | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
mysql> DESC tb_emp7;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| id     | int(11)     | NO   | PRI | NULL    |       |
| name   | varchar(25) | YES  |     | NULL    |       |
| deptId | int(11)     | YES  |     | NULL    |       |
| salary | float       | YES  |     | 0       |       |
+--------+-------------+------+-----+---------+-------+
4 rows in set (0.04 sec)
```

 【实例 2】创建一个名为 double\_salary 的触发器，触发的条件是向数据表 tb\_emp6 中插入数据之后，再向数据表 tb\_emp7 中插入相同的数据，并且 salary 为 tb\_emp6 中新插入的 salary 字段值的 2 倍。输入的 SQL 语句和执行过程如下所示。

```text
mysql> CREATE TRIGGER double_salary
    -> AFTER INSERT ON tb_emp6
    -> FOR EACH ROW
    -> INSERT INTO tb_emp7
    -> VALUES (NEW.id,NEW.name,deptId,2*NEW.salary);
Query OK, 0 rows affected (0.25 sec)
```

 触发器 double\_salary 创建完成之后，向表 tb\_emp6 中插入记录时，同时向表 tb\_emp7 中插入相同的记录，并且 salary 字段为 tb\_emp6 中 salary 字段值的 2 倍，如下所示。

```text
mysql> INSERT INTO tb_emp6
    -> VALUES (1,'A',1,1000),(2,'B',1,500);
Query OK, 2 rows affected (0.09 sec)
Records: 2  Duplicates: 0  Warnings: 0
mysql> SELECT * FROM tb_emp6;
+----+------+--------+--------+
| id | name | deptId | salary |
+----+------+--------+--------+
|  1 | A    |      1 |   1000 |
|  2 | B    |      1 |    500 |
+----+------+--------+--------+
3 rows in set (0.04 sec)
mysql> SELECT * FROM tb_emp7;
+----+------+--------+--------+
| id | name | deptId | salary |
+----+------+--------+--------+
|  1 | A    |      1 |   2000 |
|  2 | B    |      1 |   1000 |
+----+------+--------+--------+
2 rows in set (0.06 sec)
```

