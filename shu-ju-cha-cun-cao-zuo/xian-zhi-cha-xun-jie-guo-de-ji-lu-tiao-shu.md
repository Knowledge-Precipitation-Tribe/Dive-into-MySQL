# 限制查询结果的记录条数

在使用 MySQL SELECT 语句时往往返回的是所有匹配的行，有些时候我们仅需要返回第一行或者前几行，这时候就需要用到 MySQL LIMT 子句。

 基本的语法格式如下：

```text
 <LIMIT> [<位置偏移量>,] <行数>
```

 LIMIT 接受一个或两个数字参数。参数必须是一个整数常量。如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目。

 第一个参数“位置偏移量”指示 MySQL 从哪一行开始显示，是一个可选参数，如果不指定“位置偏移量”，将会从表中的第一条记录开始（第一条记录的位置偏移量是 0，第二条记录的位置偏移量是 1，以此类推）；第二个参数“行数”指示返回的记录条数。

 显示 tb\_students\_info 表查询结果的前2行，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info LIMIT 2;
```

![](../.gitbook/assets/image%20%2820%29.png)

 由结果可以看到，该语句没有指定返回记录的“位置偏移量”参数，显示结果从第一行开始，“行数”参数为 2，因此返回的结果为表中的前2行记录。

 若指定返回记录的开始位置，则返回结果为从“位置偏移量”参数开始的指定行数，“行数”参数指定返回的记录条数。

 在 tb\_students\_info 表中，使用 LIMIT 子句返回从第2条记录开始的行数为2的记录，输入的 SQL 语句和执行结果如下所示。

```text
SELECT * FROM tb_students_info LIMIT 1,2;
```

![](../.gitbook/assets/image%20%2880%29.png)

 由结果可以看到，该语句指示 MySQL 返回从第1条记录行开始的之后的2条记录，第一个数字“2”表示从第 1行开始（位置偏移量从 0 开始，第2行的位置偏移量为 1），第二个数字2表示返回的行数。

 所以，带一个参数的 LIMIT 指定从查询结果的首行开始，唯一的参数表示返回的行数，即“LIMIT n”与“LIMIT 0，n”等价。带两个参数的 LIMIT 可返回从任何位置开始的指定行数的数据。

 返回第一行时，位置偏移量是 0。因此，“LIMIT 1，1”返回第 2 行，而不是第 1 行。

> 注意：MySQL 5.7 中可以使用“LIMIT 4 OFFSET 3”，意思是获取从第5条记录开始的后面的3条记录，和“LIMIT 4，3”返回的结果相同。
