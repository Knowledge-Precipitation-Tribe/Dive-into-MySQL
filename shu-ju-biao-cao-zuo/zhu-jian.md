# 主键

“主键\(PRIMARY KEY\)”的完整称呼是“主键约束”。MySQL 主键约束是一个列或者列的组合，其值能唯一地标识表中的每一行。这样的一列或多列称为表的主键，通过它可以强制表的实体完整性。

### 选取设置主键约束的字段

主键约束即在表中定义一个主键来唯一确定表中每一行数据的标识符。主键可以是表中的某一列或者多列的组合，其中由多列组合的主键称为复合主键。主键应该遵守下面的规则：

* 每个表只能定义一个主键。
* 主键值必须唯一标识表中的每一行，且不能为 NULL，即表中不可能存在两行数据有相同的主键值。这是唯一性原则。
* 一个列名只能在复合主键列表中出现一次。
* 复合主键不能包含不必要的多余列。当把复合主键的某一列删除后，如果剩下的列构成的主键仍然满足唯一性原则，那么这个复合主键是不正确的。这是最小化原则。

### 创建表时设置主键

在CREATE TABLE语句中，主键是通过**PRIMARY KEY**关键字来指定的。语法如下：

```text
<字段名> <数据类型> PRIMARY KEY [默认值]
```

在 test\_db 数据库中创建 tb\_emp 3 数据表，其主键为 id，输入的 SQL 语句和运行结果如下所示。

```text
CREATE TABLE tb_emp3(
    id INT(11) PRIMARY KEY,
    name VARCHAR(25),
    deptId INT(11),
    salary FLOAT
);
```

或者

```text
CREATE TABLE tb_emp3(
    id INT(11),
    name VARCHAR(25),
    deptId INT(11),
    salary FLOAT,
    PRIMARY KEY(id)
);
```

```text
DESC tb_emp3;
```

![](../.gitbook/assets/image%20%2847%29.png)

### 创建表时创建复合主键

创建数据表 tb\_emp4，假设表中没有主键 id，为了唯一确定一个员工，可以把 name、deptId 联合起来作为主键，输入的 SQL 语句和运行结果如下所示。

```text
CREATE TABLE tb_emp4(
    name VARCHAR(25),
    deptId INT(11),
    salary FLOAT,
    PRIMARY KEY(name, deptId)
);
```

```text
DESC tb_emp4;
```

![](../.gitbook/assets/image%20%2831%29.png)

### 在修改表时添加主键约束

在修改数据表时添加主键约束的语法规则为：

```text
ALTER TABLE <数据表名> ADD PRIMARY KEY(<列名>);
```

查看 tb\_emp2 数据表的表结构，如下所示。

![](../.gitbook/assets/image%20%2861%29.png)

改数据表 tb\_emp2，将字段 id 设置为主键，输入的 SQL 语句和运行结果如下所示。

```text
ALTER TABLE tb_emp2 ADD PRIMARY KEY(id);
```

![](../.gitbook/assets/image%20%28103%29.png)

