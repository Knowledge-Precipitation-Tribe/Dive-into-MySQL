# 外连接查询

MySQL中内连接是在交叉连接的结果集上返回满足条件的记录；而外连接先将连接的表分为基表和参考表，再以基表为依据返回满足和不满足条件的记录。

外连接更加注重两张表之间的关系。按照连接表的顺序，可以分为左外连接和右外连接。

左外连接又称为左连接，在 FROM 子句中使用关键字 LEFT OUTER JOIN 或者 LEFT JOIN，用于接收该关键字左表（基表）的所有行，并用这些行与该关键字右表（参考表）中的行进行匹配，即匹配左表中的每一行及右表中符合条件的行。

在左外连接的结果集中，除了匹配的行之外，还包括左表中有但在右表中不匹配的行，对于这样的行，从右表中选择的列的值被设置为 NULL，即左外连接的结果集中的 NULL 值表示右表中没有找到与左表相符的记录。

在 tb\_students\_info 表和 tb\_departments 表中查询所有学生，包括没有学院的学生，输入的 SQL 语句和执行结果如下所示。

```sql
mysql> SELECT name,dept_name
    -> FROM tb_students_info s
    -> LEFT OUTER JOIN tb_departments d
    -> ON s.dept_id = d.dept_id;
+--------+-----------+
| name   | dept_name |
+--------+-----------+
| Dany   | Computer  |
| Jane   | Computer  |
| Jim    | Computer  |
| Henry  | Math      |
| John   | Math      |
| Green  | Chinese   |
| Thomas | Chinese   |
| Susan  | Economy   |
| Tom    | Economy   |
| Lily   | NULL      |
+--------+-----------+
10 rows in set (0.03 sec)
```

结果显示了 10 条记录，name 为 Lily 的学生目前没有学院，因为对应的 tb\_departments 表中并没有该学生的学院信息，所以该条记录只取出了 tb\_students\_info 表中相应的值，而从 tb\_departments 表中取出的值为 NULL。

右外连接又称为右连接，在 FROM 子句中使用 RIGHT OUTER JOIN 或者 RIGHT JOIN。与左外连接相反，右外连接以右表为基表，连接方法和左外连接相同。在右外连接的结果集中，除了匹配的行外，还包括右表中有但在左表中不匹配的行，对于这样的行，从左表中选择的值被设置为 NULL。

在 tb\_students\_info 表和 tb\_departments 表中查询所有学院，包括没有学生的学院，输入的 SQL 语句和执行结果如下所示。

```sql
mysql> SELECT name,dept_name
    -> FROM tb_students_info s
    -> RIGHT OUTER JOIN tb_departments d
    -> ON s.dept_id = d.dept_id;
+--------+-----------+
| name   | dept_name |
+--------+-----------+
| Dany   | Computer  |
| Green  | Chinese   |
| Henry  | Math      |
| Jane   | Computer  |
| Jim    | Computer  |
| John   | Math      |
| Susan  | Economy   |
| Thomas | Chinese   |
| Tom    | Economy   |
| NULL   | History   |
+--------+-----------+
10 rows in set (0.00 sec)
```

可以看到，结果只显示了 10 条记录，名称为 History 的学院目前没有学生，对应的 tb\_students\_info 表中并没有该学院的信息，所以该条记录只取出了 tb\_departments 表中相应的值，而从 tb\_students\_info 表中取出的值为 NULL。

