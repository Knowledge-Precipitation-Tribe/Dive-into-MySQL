# 对查询结果进行排序

在 MySQL SELECT 语句中，ORDER BY 子句主要用来将结果集中的数据按照一定的顺序进行排序。

 其语法格式为：

```text
 ORDER BY {<列名> | <表达式> | <位置>} [ASC|DESC]
```

 语法说明如下。

1. 列名，指定用于排序的列。可以指定多个列，列名之间用逗号分隔。
2. 表达式，指定用于排序的表达式。
3. 位置，指定用于排序的列在 SELECT 语句结果集中的位置，通常是一个正整数。
4. ，ASC\|DESC，**关键字 `ASC` 表示按升序分组，关键字 `DESC` 表示按降序分组**，其中 `ASC` 为默认值。这两个关键字必须位于对应的列名、表达式、列的位置之后。

 使用 ORDER BY 子句应该注意以下几个方面：

*  ORDER BY 子句中可以包含子查询。
*  当排序的值中存在空值时，ORDER BY 子句会将该空值作为最小值来对待。
*  当在 ORDER BY 子句中指定多个列进行排序时，MySQL 会按照列的顺序从左到右依次进行排序。
*  查询的数据并没有以一种特定的顺序显示，如果没有对它们进行排序，则将根据插入到数据表中的顺序显示。使用 ORDER BY 子句对指定的列数据进行排序。

 查询 tb\_students\_info 表的 height 字段值，并对其进行排序，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info ORDER BY height;
```

![](../.gitbook/assets/image%20%2873%29.png)

 该语句通过指定 ORDER BY 子句，MySQL 对查询的 height 列的数据按数值的大小进行了升序排序。

 有时需要根据多列进行排序。对多列数据进行排序要将需要排序的列之间用逗号隔开。

 查询 tb\_students\_info 表中的 name 和 height 字段，先按 height 排序，再按 name 排序，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info ORDER BY height, name;
```

![](../.gitbook/assets/image%20%2812%29.png)

{% hint style="info" %}
注意：在对多列进行排序时，首行排序的第一列必须有相同的列值，才会对第二列进行排序。如果第一列数据中所有的值都是唯一的，将不再对第二列进行排序
{% endhint %}

 默认情况下，查询数据按字母升序进行排序（A～Z），但数据的排序并不仅限于此，还可以使用 ORDER BY 对查询结果进行降序排序（Z～A），这可以通过关键字 DESC 实现。可以对多列进行不同的顺序排序。

查询 tb\_students\_info 表，先按 height 降序排序，再按 name 升序排序，输入的 SQL 语句和执行过程如下所示。

```text
SELECT * FROM tb_students_info ORDER BY height DESC,name ASC;
```

![](../.gitbook/assets/image%20%282%29.png)

> 注意：DESC 关键字只对前面的列进行降序排列，在这里只对 height 排序，而并没有对 name 进行排序，因此，height 按降序排序，而 name 仍按升序排序，如果要对多列进行降序排序，必须要在每一列的后面加 DESC 关键字。

