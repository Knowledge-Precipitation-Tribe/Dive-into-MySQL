# 设置别名

为了查询方便，MySQL 提供了 AS 关键字来为表和字段指定别名。本节主要讲解如何为表和字段指定一个别名。

##  为表指定别名

 当表名很长或者执行一些特殊查询的时候，为了方便操作，可以为表指定一个别名，用这个别名代替表原来的名称。

 为表指定别名的基本语法格式为：

```text
 <表名> [AS] <别名>
```

 其中各子句的含义如下：

*  `<表名>`：数据库中存储的数据表的名称。
*  `<别名>`：查询时指定的表的新名称。
*  `AS`**关键字可以省略，省略后需要将表名和别名用空格隔开。**

{% hint style="info" %}
注意：表的别名不能与该数据库的其它表同名。字段的别名不能与该表的其它字段同名。在条件表达式中不能使用字段的别名，否则会出现`“ERROR 1054 (42S22): Unknown column”`这样的错误提示信息。
{% endhint %}

 下面为 tb\_students\_info 表指定别名 stu，SQL 语句和运行结果如下。

```text
SELECT stu.name, stu.height FROM tb_students_info AS stu;
```

![](../.gitbook/assets/image%20%286%29.png)

##  为字段指定别名

 在使用 SELECT 语句查询数据时，MySQL 会显示每个 SELECT 后面指定输出的字段。有时为了显示结果更加直观，我们可以为字段指定一个别名。

 为字段指定别名的基本语法格式为：

```text
<字段名> [AS] <别名>
```

 其中，各子句的语法含义如下：

*  `<字段名>`：为数据表中字段定义的名称。
*  `<字段别名>`：字段新的名称。
*  `AS`关键字可以省略，省略后需要将字段名和别名用空格隔开。

 查询 tb\_students\_info 表，为 name 指定别名 student\_name，为 age 指定别名 student\_age，SQL 语句和运行结果如下。

```text
SELECT name AS student_name, age AS student_age FROM tb_students_info;
```

![](../.gitbook/assets/image%20%2810%29.png)

{% hint style="info" %}
注意：表别名只在执行查询时使用，并不在返回结果中显示。而字段定义别名之后，会返回给客户端显示，显示的字段为字段的别名。
{% endhint %}

