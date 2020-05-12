# 删除数据

在 MySQL 中，可以使用 DELETE 语句来删除表的一行或者多行数据。

##  删除单个表中的数据

 使用 DELETE 语句从单个表中删除数据，语法格式为：

```text
DELETE FROM <表名> [WHERE 子句] [ORDER BY 子句] [LIMIT 子句]
```

 语法说明如下：

*  `<表名>`：指定要删除数据的表名。
*  `ORDER BY` 子句：可选项。表示删除时，表中各行将按照子句中指定的顺序进行删除。
*  `WHERE` 子句：可选项。表示为删除操作限定删除条件，若省略该子句，则代表删除该表中的所有行。
*  `LIMIT` 子句：可选项。用于告知服务器在控制命令被返回到客户端前被删除行的最大值。

{% hint style="danger" %}
注意：在不使用 WHERE 条件的时候，将删除所有数据。
{% endhint %}

##  删除表中的全部数据

 【实例 1】删除 tb\_courses\_new 表中的全部数据，输入的 SQL 语句和执行结果如下所示。

```text
mysql> DELETE FROM tb_courses_new;
Query OK, 3 rows affected (0.12 sec)
mysql> SELECT * FROM tb_courses_new;
Empty set (0.00 sec)
```

##  根据条件删除表中的数据

 【实例 2】在 tb\_courses\_new 表中，删除 course\_id 为 4 的记录，输入的 SQL 语句和执行结果如下所示。

```text
DELETE FROM tb_course_new WHERE course_id=4;
```

![](../.gitbook/assets/image%20%2887%29.png)

 由运行结果可以看出，course\_id 为 4 的记录已经被删除。

