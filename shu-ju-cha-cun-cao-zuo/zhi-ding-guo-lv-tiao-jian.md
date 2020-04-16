# 指定过滤条件

在 MySQL SELECT 语句中，除了能使用 GROUP BY 子句分组数据外，还可以使用 HAVING 子句过滤分组，在结果集中规定了包含哪些分组和排除哪些分组。

 语法格式如下：

```text
HAVING <条件>
```

 其中，`<条件>`指的是指定的过滤条件。

 HAVING 子句和 WHERE 子句非常相似，HAVING 子句支持 WHERE 子句中所有的操作符和语法，但是两者存在几点差异：

*  WHERE 子句主要用于过滤数据行，而 HAVING 子句主要用于过滤分组，即 HAVING 子句基于分组的聚合值而不是特定行的值来过滤数据，主要用来过滤分组。
*  WHERE 子句不可以包含聚合函数，HAVING 子句中的条件可以包含聚合函数。
*  HAVING 子句是在数据分组后进行过滤，WHERE 子句会在数据分组前进行过滤。WHERE 子句排除的行不包含在分组中，可能会影响 HAVING 子句基于这些值过滤掉的分组。

 【实例】根据 dept\_id 对 tb\_students\_info 表中的数据进行分组，并显示学生人数大于1的分组信息，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT dept_id,GROUP_CONCAT(name) AS names
    -> FROM tb_students_info
    -> GROUP BY dept_id
    -> HAVING COUNT(name)>1;
+---------+---------------+
| dept_id | names         |
+---------+---------------+
|       1 | Dany,Jane,Jim |
|       2 | Henry,John    |
|       3 | Green,Thomas  |
|       4 | Susan,Tom     |
+---------+---------------+
4 rows in set (0.07 sec)
```

