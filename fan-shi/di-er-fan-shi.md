# 第二范式

* 数据库表中不存在非关键字段对任一候选关键字段的部分函数依赖，则符合第二范式。
* 如果一个表中某一个字段 A 的值是由另外一个字段或一组字段 B 的值来确定的，就称为 A 函数依赖于B
* 当某张表中的非主键信息不是由整个主键函数来决定时，即存在依赖于该表中不是主键的部分或者依赖于主键一部分的部分时通常会违反2NF。

在第一范式的基础上，非主键列完全依赖于主键，而不能是依赖于主键的一部分

