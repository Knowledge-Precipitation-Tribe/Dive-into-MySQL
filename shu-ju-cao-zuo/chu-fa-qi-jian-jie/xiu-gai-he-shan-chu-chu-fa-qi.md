# 修改和删除触发器

修改触发器可以通过删除原触发器，再以相同的名称创建新的触发器。

##  基本语法

 与其他 MySQL 数据库对象一样，可以使用 DROP 语句将触发器从数据库中删除。

 语法格式如下：

```text
DROP TRIGGER [ IF EXISTS ] [数据库名] <触发器名>
```

 语法说明如下：

###  1\) 触发器名

 要删除的触发器名称。

###  2\) 数据库名

 可选项。指定触发器所在的数据库的名称。若没有指定，则为当前默认的数据库。

###  3\) 权限

 执行 DROP TRIGGER 语句需要 SUPER 权限。

###  4\) IF EXISTS

 可选项。避免在没有触发器的情况下删除触发器。

> 注意：删除一个表的同时，也会自动删除该表上的触发器。另外，触发器不能更新或覆盖，为了修改一个触发器，必须先删除它，再重新创建。

##  删除触发器

 使用 DROP TRIGGER 语句可以删除 MySQL 中已经定义的触发器。

 【实例】删除 double\_salary 触发器，输入的 SQL 语句和执行过程如下所示。

```text
mysql> DROP TRIGGER double_salary;
Query OK, 0 rows affected (0.03 sec)
```

 删除 double\_salary 触发器后，再次向数据表 tb\_emp6 中插入记录时，数据表 tb\_emp7 的数据不再发生变化，如下所示。

```text
mysql> INSERT INTO tb_emp6
    -> VALUES (3,'C',1,200);
Query OK, 1 row affected (0.09 sec)
mysql> SELECT * FROM tb_emp6;
+----+------+--------+--------+
| id | name | deptId | salary |
+----+------+--------+--------+
|  1 | A    |      1 |   1000 |
|  2 | B    |      1 |    500 |
|  3 | C    |      1 |    200 |
+----+------+--------+--------+
3 rows in set (0.00 sec)
mysql> SELECT * FROM tb_emp7;
+----+------+--------+--------+
| id | name | deptId | salary |
+----+------+--------+--------+
|  1 | A    |      1 |   2000 |
|  2 | B    |      1 |   1000 |
+----+------+--------+--------+
2 rows in set (0.00 sec)
```

