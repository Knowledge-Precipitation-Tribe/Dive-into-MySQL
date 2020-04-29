# 默认值

“默认值（Default）”的完整称呼是“默认值约束（Default Constraint）”。MySQL 默认值约束用来指定某列的默认值。例如女性同学较多，性别就可以默认为“女”。如果插入一条新的记录时没有为这个字段赋值，那么系统会自动为这个字段赋值为“女”。

##  在创建表时设置默认值约束

 创建表时可以使用 **DEFAULT** 关键字设置默认值约束，具体的语法规则如下：

```text
<字段名> <数据类型> DEFAULT <默认值>;
```

 创建数据表 tb\_dept3，指定部门位置默认为 Beijing，输入的 SQL 语句和运行结果如下所示。

```text
CREATE TABLE tb_dept3(
    id INT(11) PRIMARY KEY,
    name VARCHAR(22),
    location VARCHAR(50) DEFAULT 'Beijing'
);
```

 

![](../.gitbook/assets/image%20%2811%29.png)

以上语句执行成功之后，表 tb\_dept3 上的字段 location 拥有了一个默认值 Beijing，新插入的记录如果没有指定部门位置，则默认都为 Beijing。

##  在修改表时添加默认值约束

 修改表时添加默认值约束的语法规则如下：

```text
ALTER TABLE <数据表名> CHANGE COLUMN <字段名> <数据类型> DEFAULT <默认值>;
```

修改数据表 tb\_dept3，将部门位置的默认值修改为 Shanghai，输入的 SQL 语句和运行结果如下所示。

```text
ALTER TABLE tb_dept3 CHANGE COLUMN  location location VARCHAR(50) DEFAULT 'shanghai';
```

![](../.gitbook/assets/image%20%28117%29.png)

##  删除默认值约束

 修改表时删除默认值约束的语法规则如下：

```text
 ALTER TABLE <数据表名>
 CHANGE COLUMN <字段名> <字段名> <数据类型> DEFAULT NULL;
```

 修改数据表 tb\_dept3，将部门位置的默认值约束删除，输入的 SQL 语句和运行结果如下所示。

```text
ALTER TABLE tb_dept3 CHANGE COLUMN location location VARCHAR(50) DEFAULT NULL;
```

![](../.gitbook/assets/image%20%28124%29.png)

