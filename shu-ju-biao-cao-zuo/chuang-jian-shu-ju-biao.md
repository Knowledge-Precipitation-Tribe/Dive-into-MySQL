# 创建数据表

在MySQL中使用\`CREATE TABLE\`语句创建表。语法格式为：

```text
CREATE TABLE <表名> (<列名1><类型>, <列名2><类型>, ...)
```

{% hint style="info" %}
要创建的表的名称不区分大小写，不能使用SQL语言中的关键字，如DROP、ALTER、INSERT等。
{% endhint %}

数据表属于数据库，在创建数据表之前，应使用语句“USE&lt;数据库&gt;”指定操作在哪个数据库中进行，如果没有选择数据库，就会抛出 No database selected 的错误。

### 案例

创建员工表 tb\_emp1，结构如下表所示。

![](../.gitbook/assets/image%20%2821%29.png)

```text
CREATE TABLE tb_emp1(
    id INT(11),
    name VARCHAR(25),
    deptId INT(11),
    salary FLOAT
);
```

![](../.gitbook/assets/image%20%2822%29.png)

使用命令查看数据表

```text
SHOW TABLES;
```

![](../.gitbook/assets/image%20%2831%29.png)

查看表的结构

```text
DESCRIBE tb_emp1;
```

![](../.gitbook/assets/image%20%2811%29.png)

其中，各个字段的含义如下：

* Null：表示该列是否可以存储 NULL 值。
* Key：表示该列是否已编制索引。PRI 表示该列是表主键的一部分，UNI 表示该列是 UNIQUE 索引的一部分，MUL 表示在列中某个给定值允许出现多次。
* Default：表示该列是否有默认值，如果有，值是多少。
* Extra：表示可以获取的与给定列有关的附加信息，如 AUTO\_INCREMENT 等。

