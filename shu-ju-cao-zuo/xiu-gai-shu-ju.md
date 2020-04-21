# 修改数据

在 MySQL 中，可以使用 UPDATE 语句来修改、更新一个或多个表的数据。

##  UPDATE 语句的基本语法

 使用 UPDATE 语句修改单个表，语法格式为：

```text
UPDATE <表名> SET 字段1=值1 [,字段2=值2… ] [WHERE 子句 ] [ORDER BY 子句] [LIMIT 子句]
```

 语法说明如下：

*  `<表名>`：用于指定要更新的表名称。
*  `SET` 子句：用于指定表中要修改的列名及其列值。其中，每个指定的列值可以是表达式，也可以是该列对应的默认值。如果指定的是默认值，可用关键字 DEFAULT 表示列值。
*  `WHERE` 子句：可选项。用于限定表中要修改的行。若不指定，则修改表中所有的行。
*  `ORDER BY` 子句：可选项。用于限定表中的行被修改的次序。
*  `LIMIT` 子句：可选项。用于限定被修改的行数。

> 注意：修改一行数据的多个列值时，SET 子句的每个值用逗号分开即可。

##  修改表中的数据

 【实例 1】在 tb\_courses\_new 表中，更新所有行的 course\_grade 字段值为 4，输入的 SQL 语句和执行结果如下所示。

```text
UPDATE tb_course_new SET course_grade=4;
```

![](../.gitbook/assets/image%20%28124%29.png)

{% hint style="info" %}
update语句需要加入where限定条件，否则会对整个表进行更新，操作不当容易导致数据丢失。
{% endhint %}

##  根据条件修改表中的数据

 【实例 2】在 tb\_courses\_new 表中，更新 course\_id 值为 2 的记录，将 course\_grade 字段值改为 3.5，将 course\_name 字段值改为“DB”，输入的 SQL 语句和执行结果如下所示。

```text
UPDATE tb_course_new SET course_name='DB', course_grade=3.5 WHERE course_id=2;
```

![](../.gitbook/assets/image%20%288%29.png)

 注意：保证 UPDATE 以 WHERE 子句结束，通过 WHERE 子句指定被更新的记录所需要满足的条件，如果忽略 WHERE 子句，MySQL 将更新表中所有的行。

