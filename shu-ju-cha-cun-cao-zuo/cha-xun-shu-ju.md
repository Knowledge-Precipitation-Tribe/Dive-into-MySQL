# 查询数据

在 MySQL 中，可以使用 SELECT 语句来查询数据。查询数据是指从数据库中根据需求，使用不同的查询方式来获取不同的数据，是使用频率最高、最重要的操作。

SELEC的语法格式如下：

```text
SELECT
{* | <字段列名>}
[
FROM <表 1>, <表 2>…
[WHERE <表达式>
[GROUP BY <group by definition>
[HAVING <expression> [{<operator> <expression>}…]]
[ORDER BY <order by definition>]
[LIMIT[<offset>,] <row count>]
]
```

其中，各条子句的含义如下：

* `{*|<字段列名>}`包含星号通配符的字段列表，表示所要查询字段的名称。
* `<表 1>，<表 2>…`，表 1 和表 2 表示查询数据的来源，可以是单个或多个。
* `WHERE <表达式>`是可选项，如果选择该项，将限定查询数据必须满足该查询条件。
* `GROUP BY< 字段 >`，该子句告诉 MySQL 如何显示查询出来的数据，并按照指定的字段分组。
* `[ORDER BY< 字段 >]`，该子句告诉 MySQL 按什么样的顺序显示查询出来的数据，可以进行的排序有升序（ASC）和降序（DESC），默认情况下是升序。
* `[LIMIT[<offset>，]<row count>]`，该子句告诉 MySQL 每次显示查询出来的数据条数。

下面先介绍一些简单的 SELECT 语句，关于 WHERE、GROUP BY、ORDER BY 和 LIMIT 等限制条件，后面我们会一一讲解。

### 准备数据

```text
CREATE TABLE tb_students_info(
    id INT(11) PRIMARY KEY,
    name VARCHAR(22) UNIQUE,
    deptId INT(11) NOT NULL,
    age INT(11) NOT NULL,
    sex VARCHAR(22),
    height FLOAT,
    login_data DATE
);
```

```text
INSERT INTO tb_students_info
    (id, name, deptId, age, sex, height, login_data)
    values
    (1, 'Dany', 1, 25, 'F', 160, '2015-09-10');
INSERT INTO tb_students_info
    (id, name, deptId, age, sex, height, login_data)
    values
    (2, 'Green', 3, 23, 'F', 158, '2016-10-2');
INSERT INTO tb_students_info
    (id, name, deptId, age, sex, height, login_data)
    values
    (3, 'Henry', 2, 23, 'M', 185, '2015-05-31');
```

### 查询表中所有字段

查询所有字段是指查询表中所有字段的数据。MySQL 提供了以下 2 种方式查询表中的所有字段。

* 使用“\*”通配符查询所有字段
* 列出表的所有字段

#### **1）使用“\*”查询表的所有字段**

SELECT 可以使用“\*”查找表中所有字段的数据，语法格式如下：

```text
SELECT * FROM 表名;
```

使用“\*”查询时，只能按照数据表中字段的顺序进行排列，不能改变字段的排列顺序。

从 tb\_students\_info 表中查询所有字段的数据，SQL 语句和运行结果如下所示。

```text
SELECT * FROM FROM tb_students_info
```

![](../.gitbook/assets/image%20%2827%29.png)

结果显示，使用“\*”通配符时，将返回所有列，数据列按照创建表时的顺序显示。

{% hint style="info" %}
一般情况下，除非需要使用表中所有的字段数据，否则最好不要使用通配符“_”。虽然使用通配符可以节省输入查询语句的时间，但是获取不需要的列数据通常会降低查询和所使用的应用程序的效率。使用“_”的优势是，当不知道所需列的名称时，可以通过“\*”获取它们。
{% endhint %}

#### **2）列出表的所有字段**

SELECT 关键字后面的字段名为需要查找的字段，因此可以将表中所有字段的名称跟在 SELECT 关键字后面。如果忘记了字段名称，可以使用 DESC 命令查看表的结构。有时，由于表的字段比较多，不一定能记得所有字段的名称，因此该方法很不方便，不建议使用。

查询 tb\_students\_info 表中的所有数据，SQL 语句还可以书写如下：

```text
SELECT (id,name,dept_id,age,sex,height,login_date) FROM tb_students_info;
```

![](../.gitbook/assets/image%20%2827%29.png)

这种查询方式比较灵活，如果需要改变字段显示的顺序，只需调整 SELECT 关键字后面的字段列表顺序即可。虽然列出表的所有字段的方式比较灵活，但是查询所有字段时通常使用“_”通配符。使用“_”这种方式比较简单，尤其是表中的字段很多的时候，这种方式的优势更加明显。当然，如果需要改变字段显示的顺序，可以选择列出表的所有字段。

### 查询表中指定的字段

```text
SELECT < 列名 > FROM < 表名 >;
```

查询 tb\_students\_info 表中 name 列所有学生的姓名，SQL 语句和运行结果如下所示。

```text
SELECT name FROM tb_students_info;
```

![](../.gitbook/assets/image%20%2852%29.png)

从 tb\_students\_info 表中获取 id、name 和 height 三列，SQL 语句和运行结果如下所示。

```text
SELECT id, name, height FROM tb_students_info;
```

![](../.gitbook/assets/image%20%2844%29.png)

