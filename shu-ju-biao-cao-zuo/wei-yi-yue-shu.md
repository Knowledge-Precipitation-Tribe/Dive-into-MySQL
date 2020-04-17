# 唯一约束

MySQL唯一约束（Unique Key）要求该列唯一，允许为空，但只能出现一个空值。唯一约束可以确保一列或者几列不出现重复值。

### 在创建表时设置唯一约束

在定义完列之后直接使用 **UNIQUE** 关键字指定唯一约束，语法规则如下：

```text
<字段名> <数据类型> UNIQUE
```

创建数据表 tb\_dept2，指定部门的名称唯一，输入的 SQL 语句和运行结果如下所示。

```text
CREATE TABLE tb_dept2(
    id INT(11) PRIMARY KEY,
    name VARCHAR(22) UNIQUE,
    location VARCHAR(50)
);
```

![](../.gitbook/assets/image%20%2866%29.png)

{% hint style="info" %}
UNIQUE 和 PRIMARY KEY 的区别：一个表可以有多个字段声明为 UNIQUE，但只能有一个 PRIMARY KEY 声明；声明为 PRIMAY KEY 的列不允许有空值，但是声明为 UNIQUE 的字段允许空值的存在。
{% endhint %}

### 在修改表时添加唯一约束

在修改表时添加唯一约束的语法格式为：

```text
ALTER TABLE <数据表名> ADD CONSTRAINT <唯一约束名> UNIQUE(<列名>);
```

修改数据表 tb\_dept1，指定部门的名称唯一，输入的 SQL 语句和运行结果如下所示。

```text
ALTER TABLE tb_dept1 ADD CONSTRAINT unique_name UNIQUE(name);
```

![](../.gitbook/assets/image%20%2817%29.png)

### 删除唯一约束

在MySQL中删除唯一约束的语法格式如下：

```text
ALTER TABLE <表名> DROP INDEX <唯一约束名>;
```

删除数据表tb\_dept1中的唯一约束unique\_name，输入的SQL语句和运行结果如下所示。

```text
ALTER TABLE tb_dept1 DROP INDEX unique_name;
```

![](../.gitbook/assets/image%20%2818%29.png)

