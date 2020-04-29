# 查看表中的约束

在 MySQL 中可以使用 SHOW CREATE TABLE 语句来查看表中的约束。查看数据表中的约束语法格式如下：

```text
SHOW CREATE TABLE <数据表名>;
```

 创建数据表 tb\_emp8 并指定 id 为主键约束，name 为唯一约束，deptId 为非空约束和外键约束，然后查看表中的约束，输入SQL语句运行结果如下。

```text
CREATE TABLE tb_emp8(
    id INT(11) PRIMARY KEY,
    name VARCHAR(22) UNIQUE,
    deptId INT(11) NOT NULL,
    salary FLOAT DEFAULT 0,
    CHECK ( salary>0 ),
    FOREIGN KEY(deptId) REFERENCES tb_dept1(id)
);
```

![](../.gitbook/assets/image%20%28110%29.png)

