# DENSE\_RANK\(\)

> 转载自：[https://www.begtut.com/mysql/mysql-dense\_rank-function.html](https://www.begtut.com/mysql/mysql-dense_rank-function.html)

## DENSE\_RANK函数简介

`DENSE_RANK()`是一个窗口函数，它为分区或结果集中的每一行分配排名，而排名值没有间隙。行的等级从行前的不同等级值的数量增加1。

`DENSE_RANK()` 函数的语法如下：

```sql
DENSE_RANK() OVER (
    PARTITION BY [{,...}]
    ORDER BY  [ASC|DESC], [{,...}]
)
```

在这个语法中：

* 首先，`PARTITION BY`子句将`FROM`子句生成的结果集划分为分区。`DENSE_RANK()`函数应用于每个分区。
* 其次，`ORDER BY`  子句指定`DENSE_RANK()`函数操作的每个分区中的行顺序。

如果分区具有两个或更多具有相同排名值的行，则将为这些行中的每一行分配相同的排名。

与[`RANK()`](https://www.begtut.com/mysql/mysql-window-functions/mysql-rank-function/)函数不同，`DENSE_RANK()`函数始终返回连续的排名值。

假设我们有一个`t`包含一些样本数据的表，如下所示：

```sql
CREATE TABLE rankDemo (
    val INT
);
 
INSERT INTO rankDemo(val)
VALUES(1),(2),(2),(3),(4),(4),(5);
 
 
SELECT 
    *
FROM
    rankDemo;
```

```text
+------+
| val  |
+------+
|    1 |
|    2 |
|    2 |
|    3 |
|    4 |
|    4 |
|    5 |
+------+
7 rows in set (0.02 sec)
```

以下语句使用`DENSE_RANK()`函数为每行分配排名：

```text
SELECT
    val,
    DENSE_RANK() OVER (
        ORDER BY val
    ) my_rank
FROM
    rankDemo;
```

这是输出：

```text
+------+---------+
| val  | my_rank |
+------+---------+
|    1 |       1 |
|    2 |       2 |
|    2 |       2 |
|    3 |       3 |
|    4 |       4 |
|    4 |       4 |
|    5 |       5 |
+------+---------+
7 rows in set (0.03 sec)
```

## MySQL DENSE\_RANK\(\) 函数示例

我们将使用窗口函数教程`sales`中创建的表进行演示。

```sql
mysql> select * from sales;
+----------------+-------------+--------+
| sales_employee | fiscal_year | sale   |
+----------------+-------------+--------+
| Alice          |        2016 | 150.00 |
| Alice          |        2017 | 100.00 |
| Alice          |        2018 | 200.00 |
| Bob            |        2016 | 100.00 |
| Bob            |        2017 | 150.00 |
| Bob            |        2018 | 200.00 |
| John           |        2016 | 200.00 |
| John           |        2017 | 150.00 |
| John           |        2018 | 250.00 |
+----------------+-------------+--------+
9 rows in set (0.00 sec)
```

以下声明使用`DENSE_RANK()`功能按销售额对销售员工进行排名。

```sql
SELECT
    sales_employee,
    fiscal_year,
    sale,
    DENSE_RANK() OVER (PARTITION BY
                     fiscal_year
                 ORDER BY
                     sale DESC
                ) sales_rank
FROM
    sales;
```

输出如下：

```text
+----------------+-------------+--------+------------+
| sales_employee | fiscal_year | sale   | sales_rank |
+----------------+-------------+--------+------------+
| John           |        2016 | 200.00 |          1 |
| Alice          |        2016 | 150.00 |          2 |
| Bob            |        2016 | 100.00 |          3 |
| Bob            |        2017 | 150.00 |          1 |
| John           |        2017 | 150.00 |          1 |
| Alice          |        2017 | 100.00 |          2 |
| John           |        2018 | 250.00 |          1 |
| Alice          |        2018 | 200.00 |          2 |
| Bob            |        2018 | 200.00 |          2 |
+----------------+-------------+--------+------------+
9 rows in set (0.01 sec)
```

在这个例子中：

* 首先，`PARTITION BY`子句使用会计年度将结果集划分为分区。
* 其次，`ORDER BY`条款按销售额的降序指定了销售员工的顺序。
* 第三，`DENSE_RANK()`函数应用于具有`ORDER BY`子句指定的行顺序的每个分区。



