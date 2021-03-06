# 聚集函数

我们经常需要汇总数据而不用把它们实际检索出来，为此MySQL提 供了专门的函数。使用这些函数，MySQL查询可用于检索数据，以便分 析和报表生成。这种类型的检索例子有以下几种。

* 确定表中行数（或者满足某个条件或包含某个特定值的行数）。
* 获得表中行组的和。
* 找出表列（或所有行或某些特定的行）的最大值、最小值和平均值。

上述例子都需要对表中数据（而不是实际数据本身）汇总。因此， 返回实际表数据是对时间和处理资源的一种浪费（更不用说带宽了）。重复一遍，实际想要的是汇总信息。

为方便这种类型的检索，MySQL给出了5个聚集函数。 这些函数能进行上述罗列的检索。

![](../../../.gitbook/assets/image%20%2846%29.png)

