# 非空约束

MySQL 非空约束（NOT NULL）可以通过 CREATE TABLE 或 ALTER TABLE 语句实现。在表中某个列的定义后加上关键字 NOT NULL 作为限定词，来约束该列的取值不能为空。非空约束（Not Null Constraint）指字段的值不能为空。对于使用了非空约束的字段，如果用户在添加数据时没有指定值，数据库系统就会报错。

##  在创建表时设置非空约束

 创建表时可以使用 **NOT NULL** 关键字设置非空约束，具体的语法规则如下：

```text
<字段名> <数据类型> NOT NULL;
```

创建数据表 tb\_dept4，指定部门名称不能为空，输入的 SQL 语句和运行结果如下所示。

```text
CREATE TABLE tb_dept4(
    id INT(11) PRIMARY KEY,
    name VARCHAR(22) NOT NULL,
    location VARCHAR(50)
);
```

![](../.gitbook/assets/image%20%2812%29.png)

##  在修改表时添加非空约束

 修改表时设置非空约束的语法规则如下：

```text
ALTER TABLE <数据表名> CHANGE COLUMN <字段名> <字段名> <数据类型> NOT NULL;
```

修改数据表 tb\_dept4，指定部门位置不能为空，输入的 SQL 语句和运行结果如下所示。

```text
ALTER TABLE tb_dept4 CHANGE COLUMN location location VARCHAR(50) NOT NULL;
```

![](../.gitbook/assets/image%20%2853%29.png)

##  删除非空约束

 修改表时删除非空约束的语法规则如下：

```text
ALTER TABLE <数据表名> CHANGE COLUMN <字段名> <字段名> <数据类型> NULL;
```

 修改数据表 tb\_dept4，将部门位置的非空约束删除，输入的 SQL 语句和运行结果如下所示。

```text
ALTER TABLE tb_dept4 CHANGE COLUMN location location VARCHAR(50) NULL;
```

![](../.gitbook/assets/image%20%2812%29.png)

