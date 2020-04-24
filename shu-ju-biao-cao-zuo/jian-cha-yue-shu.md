# 检查约束

MySQL 检查约束（CHECK）可以通过 CREATE TABLE 或 ALTER TABLE 语句实现，根据用户实际的完整性要求来定义。它可以分别对列或表实施 CHECK 约束。

##  选取设置检查约束的字段

 检查约束使用 **CHECK** 关键字，具体的语法格式如下：

```text
CHECK <表达式>
```

 其中：`<表达式>`指的就是 SQL 表达式，用于指定需要检查的限定条件。

 若将 CHECK 约束子句置于表中某个列的定义之后，则这种约束也称为基于列的 CHECK 约束。

 在更新表数据的时候，系统会检查更新后的数据行是否满足 CHECK 约束中的限定条件。MySQL 可以使用简单的表达式来实现 CHECK 约束，也允许使用复杂的表达式作为限定条件，例如在限定条件中加入子查询。

> 注意：若将 CHECK 约束子句置于所有列的定义以及主键约束和外键定义之后，则这种约束也称为基于表的 CHECK 约束。该约束可以同时对表中多个列设置限定条件。

##  在创建表时设置检查约束

 创建表时设置检查约束的语法规则如下：

```text
CHECK(<检查约束>)
```

 【实例 1】在 test\_db 数据库中创建 tb\_emp7 数据表，要求 salary 字段值大于 0 且小于 10000，输入的 SQL 语句和运行结果如下所示。

```text
mysql> CREATE TABLE tb_emp7
    -> (
    -> id INT(11) PRIMARY KEY,
    -> name VARCHAR(25),
    -> deptId INT(11),
    -> salary FLOAT,
    -> CHECK(salary>0 AND salary<100),
    -> FOREIGN KEY(deptId) REFERENCES tb_dept1(id)
    -> );
Query OK, 0 rows affected (0.37 sec)
```

##  在修改表时添加检查约束

 修改表时设置检查约束的语法规则如下：

```text
ALTER TABLE tb_emp7 ADD CONSTRAINT <检查约束名> CHECK(<检查约束>)
```

 【实例 2】修改 tb\_dept 数据表，要求 id 字段值大于 0，输入的 SQL 语句和运行结果如下所示。

```text
mysql> ALTER TABLE tb_emp7
    -> ADD CONSTRAINT check_id
    -> CHECK(id>0);
Query OK, 0 rows affected (0.19 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

##  删除检查约束

 修改表时删除检查约束的语法规则如下：

```text
ALTER TABLE <数据表名> DROP CONSTRAINT <检查约束名>;
```

