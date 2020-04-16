# 分组查询

在 MySQL SELECT 语句中，允许使用 GROUP BY 子句，将结果集中的数据行根据选择列的值进行逻辑分组，以便能汇总表内容的子集，实现对每个组而不是对整个结果集进行整合。

 语法格式如下：

```text
GROUP BY { <列名> | <表达式> | <位置> } [ASC | DESC]
```

 语法说明如下：

*  `<列名>`：指定用于分组的列。可以指定多个列，彼此间用逗号分隔。
*  `<表达式>`：指定用于分组的表达式。通常与聚合函数一块使用，例如可将表达式 COUNT\(\*\)AS' 人数 ' 作为 SELECT 选择列表清单的一项。
*  `<位置>`：指定用于分组的选择列在 SELECT 语句结果集中的位置，通常是一个正整数。例如，GROUP BY 2 表示根据 SELECT 语句列清单上的第 2 列的值进行逻辑分组。
*  `ASC|DESC`：关键字 ASC 表示按升序分组，关键字 DESC 表示按降序分组，其中 ASC 为默认值，注意这两个关键字必须位于对应的列名、表达式、列的位置之后。

> 注意：GROUP BY 子句中的各选择列必须也是 SELECT 语句的选择列清单中的一项。

 对于 GROUP BY 子句的使用，需要注意以下几点。

*  GROUP BY 子句可以包含任意数目的列，使其可以对分组进行嵌套，为数据分组提供更加细致的控制。
*  GROUP BY 子句列出的每个列都必须是检索列或有效的表达式，但不能是聚合函数。若在 SELECT 语句中使用表达式，则必须在 GROUP BY 子句中指定相同的表达式。
*  除聚合函数之外，SELECT 语句中的每个列都必须在 GROUP BY 子句中给出。
*  若用于分组的列中包含有 NULL 值，则 NULL 将作为一个单独的分组返回；若该列中存在多个 NULL 值，则将这些 NULL 值所在的行分为一组。

 【实例】根据 dept\_id 对 tb\_students\_info 表中的数据进行分组，将每个学院的学生姓名显示出来，输入的SQL语句和执行结果如下所示。

```text
mysql> SELECT dept_id,GROUP_CONCAT(name) AS names
    -> FROM tb_students_info
    -> GROUP BY dept_id;
+---------+---------------+
| dept_id | names         |
+---------+---------------+
|       1 | Dany,Jane,Jim |
|       2 | Henry,John    |
|       3 | Green,Thomas  |
|       4 | Susan,Tom     |
|       6 | Lily          |
+---------+---------------+
5 rows in set (0.02 sec)
```

 由运行结果可以看出，根据 dept\_id 的不同分别统计了 dept\_id 相同的姓名。

