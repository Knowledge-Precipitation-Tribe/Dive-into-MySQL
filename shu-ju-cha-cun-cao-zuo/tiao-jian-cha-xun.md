# 条件查询

在使用 MySQL SELECT语句时，可以使用 WHERE 子句来指定查询条件，从 FROM 子句的中间结果中选取适当的数据行，达到数据过滤的效果。

 语法格式如下：

```text
WHERE <查询条件> {<判定运算1>，<判定运算2>，…}
```

 其中，判定运算其结果取值为 TRUE、FALSE 和 UNKNOWN。

 判定运算的语法分类如下：

*  &lt;表达式1&gt;`{=|<|<=|>|>=|<=>|<>|！=}`&lt;表达式2&gt;
*  &lt;表达式1&gt;`[NOT]LIKE`&lt;表达式2&gt;
*  &lt;表达式1&gt;`[NOT][REGEXP|RLIKE]`&lt;表达式2&gt;
*  &lt;表达式1&gt;`[NOT]BETWEEN`&lt;表达式2&gt;`AND`&lt;表达式3&gt;
*  &lt;表达式1&gt;`IS[NOT]NULL`

##  单一条件的查询语句

在表 tb\_students\_info 中查询身高为 160cm 的学生的姓名，输入的 SQL 语句和行结果如下所示。

```text
SELECT * FROM tb_students_info WHERE height=160;
```

![](../.gitbook/assets/image%20%2822%29.png)

 该语句采用了简单的相等过滤，查询一个指定列 height 的具体值 160。

 查询年龄小于 24 的学生的姓名，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info WHERE age<24;
```

![](../.gitbook/assets/image%20%28114%29.png)

 可以看到，查询结果中所有记录的 age 字段的值均小于 24 岁，而大于或等于 24 岁的记录没有被返回。

##  多条件的查询语句

 使用 SELECT 查询时，可以增加查询的限制条件，这样可以使查询的结果更加精确。MySQL 在 WHERE 子句中使用 AND 操作符限定只有满足所有查询条件的记录才会被返回。

 可以使用 AND 连接两个甚至多个查询条件，多个条件表达式之间用 AND 分开。

 在 tb\_students\_info 表中查询 age 大于 22，并且 height小于等于 180 的学生的信息，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info WHERE age>22 AND height<180;
```

![](../.gitbook/assets/image%20%2866%29.png)

> 注意：上例的 WHERE 子句中只包含一个 AND 语句，把两个过滤条件组合在一起，实际上可以添加多个 AND 过滤条件，增加条件的同时增加一个 AND 关键字。

##  使用 LIKE 的模糊查询

 字符串匹配的语法格式如下：

```text
<表达式1> [NOT] LIKE <表达式2>
```

字符串匹配是一种模式匹配，使用运算符 LIKE 设置过滤条件，过滤条件使用通配符进行匹配运算，而不是判断是否相等进行比较。

相互间进行匹配运算的对象可以是 CHAR、VARCHAR、TEXT、DATETIME 等数据类型。运算返回的结果是 TRUE 或 FALSE。

利用通配符可以在不完全确定比较值的情形下创建一个比较特定数据的搜索模式，并置于关键字 LIKE 之后。可以在搜索模式的任意位置使用通配符，并且可以使用多个通配符。MySQL 支持的通配符有以下两种：

###  1\) 百分号（%）

 百分号%是 MySQL 中常用的一种通配符，在过滤条件中，百分号可以表示任何字符串，并且该字符串可以出现任意次。

 使用百分号通配符要注意以下几点：

*  MySQL 默认是不区分大小写的，若要区分大小写，则需要更换字符集的校对规则。
*  百分号不匹配空值。
*  百分号可以代表搜索模式中给定位置的 0 个、1 个或多个字符。
*  尾空格可能会干扰通配符的匹配，一般可以在搜索模式的最后附加一个百分号。

###  2\) 下划线（\_）

 下划线通配符和百分号通配符的用途一样，下画线只匹配单个字符，而不是多个字符，也不是 0 个字符。

> 注意：不要过度使用通配符，对通配符检索的处理一般会比其他检索方式花费更长的时间。

 在 tb\_students\_info 表中，查找所有包含“e”字母的学生姓名，输入的 SQL 的语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info WHERE name LIKE '%e%';
```

![](../.gitbook/assets/image%20%2810%29.png)

 由执行结果可以看出，该语句查询字符串中包含字母 e 的学生的姓名，只要名字中有字母 e，其前面或后面无论有多少个字符，都满足查询的条件。

## 日期字段作为条件的查询语句

以日期字段作为条件，可以使用比较运算符设置查询条件，也可以使用 BETWEEN AND 运算符查询某个范围内的值。

BETWEEN AND 用来查询某个范围内的值，该操作符需要两个参数，即范围的开始值和结束值，若字段值满足指定的范围查询条件，则这些记录被返回。

在表 tb\_students\_info 中查询注册日期在 2016-01-01 之前的学生的信息，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info WHERE login_data<'2016-01-01';
```

在表 tb\_students\_info 中查询注册日期在 2015-09-01 和 2016-12-01 之间的学生的信息，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info WHERE login_data BETWEEN '2015-09-01' AND '2016-12-01';
```

![](../.gitbook/assets/image%20%2898%29.png)

