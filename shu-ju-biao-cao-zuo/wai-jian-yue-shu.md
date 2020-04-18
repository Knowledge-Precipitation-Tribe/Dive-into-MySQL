# 外键约束

MySQL 外键约束（FOREIGN KEY）用来在两个表的数据之间建立链接，它可以是一列或者多列。一个表可以有一个或多个外键。外键对应的是参照完整性，一个表的外键可以为空值，若不为空值，则每一个外键的值必须等于另一个表中主键的某个值。外键是表的一个字段，不是本表的主键，但对应另一个表的主键。定义外键后，不允许删除另一个表中具有关联关系的行。  
外键的主要作用是保持数据的一致性、完整性。例如，部门表 tb\_dept 的主键是 id，在员工表 tb\_emp5 中有一个键 deptId 与这个 id 关联。

* 主表（父表）：对于两个具有关联关系的表而言，相关联字段中主键所在的表就是主表。
* 从表（子表）：对于两个具有关联关系的表而言，相关联字段中外键所在的表就是从表。

### 设置外键规则

定义一个外键时，需要遵守下列规则：

* 父表必须已经存在于数据库中，或者是当前正在创建的表。如果是后一种情况，则父表与子表是同一个表，这样的表称为自参照表，这种结构称为自参照完整性。
* 必须为父表定义主键。
* 主键不能包含空值，但允许在外键中出现空值。也就是说，只要外键的每个非空值出现在指定的主键中，这个外键的内容就是正确的。
* 在父表的表名后面指定列名或列名的组合。这个列或列的组合必须是父表的主键或候选键。
* 外键中列的数目必须和父表的主键中列的数目相同。
* 外键中列的数据类型必须和父表主键中对应列的数据类型相同。

### 在创建表时设置外键约束

在数据表中创建外键使用 **FOREIGN KEY** 关键字，具体的语法规则如下：

```text
[CONSTRAINT <外键名>] FOREIGN KEY 字段名 [，字段名2，...] REFERENCES <主表名> 主键列1 [，主键列2，...]
```

其中：`外键名`为定义的外键约束的名称，一个表中不能有相同名称的外键；`字段名`表示子表需要添加外健约束的字段列；`主表名`即被子表外键所依赖的表的名称；`主键列`表示主表中定义的主键列或者列组合。

为了展现表与表之间的外键关系，本例在 test\_db 数据库中创建一个部门表 tb\_dept1。

```text
CREATE TABLE tb_dept1(
    id INT(11) PRIMARY KEY,
    name VARCHAR(22) NOT NULL,
    location VARCHAR(50)
);
```

![](../.gitbook/assets/image%20%28117%29.png)

创建数据表 tb\_emp6，并在表 tb\_emp6 上创建外键约束，让它的键 deptId 作为外键关联到表 tb\_dept1 的主键 id，输入的 SQL 语句和运行结果如下所示。

```text
CREATE TABLE tb_emp6(
    id INT(11) PRIMARY KEY,
    name VARCHAR(25),
    deptId INT(11),
    salary FLOAT,
    CONSTRAINT fk_emp_dept1 FOREIGN KEY(deptId) REFERENCES tb_dept1(id)
);
```

![](../.gitbook/assets/image%20%2833%29.png)

以上语句执行成功之后，在表 tb\_emp6 上添加了名称为 fk\_emp\_dept1 的外键约束，外键名称为 deptId，其依赖于表 tb\_dept1 的主键 id。

### 在修改表时添加外键约束

在修改数据表时添加外键约束的语法规则为：

```text
ALTER TABLE <数据表名> ADD CONSTRAINT <索引名> FOREIGN KEY(<列名>) REFERENCES <主表名> (<列名>);
```

修改数据表 tb\_emp2，将字段 deptId 设置为外键，与数据表 tb\_dept1 的主键 id 进行关联，输入的 SQL 语句和运行结果如下所示。

![](../.gitbook/assets/image%20%2889%29.png)

```text
ALTER TABLE tb_emp2 ADD CONSTRAINT fk_tb_dept1 FOREIGN KEY(deptId) REFERENCES tb_dept1(id);
```

![](../.gitbook/assets/image%20%2817%29.png)

### 删除外键约束

对于数据库中定义的外键，如果不再需要，可以将其删除。外键一旦删除，就会解除主表和从表间的关联关系，MySQL 中删除外键的语法格式如下：

```text
ALTER TABLE <表名> DROP FOREIGN KEY <外键约束名>;
```

删除数据表 tb\_emp2 中的外键约束 fk\_tb\_dept1，输入的 SQL 语句和运行结果如下所示。

```text
ALTER TABLE tb_emp2 DROP FOREIGN KEY fk_tb_dept1;
```

可以看到，tb\_emp2 中已经不存在 FOREIGN KEY，原有的名称为 fk\_emp\_dept 的外键约束删除成功。

