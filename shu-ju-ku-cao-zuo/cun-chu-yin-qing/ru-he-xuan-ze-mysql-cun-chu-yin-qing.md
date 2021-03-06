# 如何选择 MySQL 存储引擎

不同的存储引擎都有各自的特点，以适应不同的需求，如表所示。为了做出选择，首先要考虑每一个存储引擎提供了哪些不同的功能。

| 功能 | MylSAM | MEMORY | InnoDB | Archive |
| :--- | :--- | :--- | :--- | :--- |
| 存储限制 | 256TB | RAM | 64TB | None |
| 支持事务 | No | No | Yes | No |
| 支持全文索引 | Yes | No | No | No |
| 支持树索引 | Yes | Yes | Yes | No |
| 支持哈希索引 | No | Yes | No | No |
| 支持数据缓存 | No | N/A | Yes | No |
| 支持外键 | No | No | Yes | No |

可以根据以下的原则来选择 MySQL 存储引擎：

* 如果要提供提交、回滚和恢复的事务安全（ACID 兼容）能力，并要求实现并发控制，InnoDB 是一个很好的选择。
* 如果数据表主要用来插入和查询记录，则 MyISAM 引擎提供较高的处理效率。
* 如果只是临时存放数据，数据量不大，并且不需要较高的数据安全性，可以选择将数据保存在内存的 MEMORY 引擎中，MySQL 中使用该引擎作为临时表，存放查询的中间结果。
* 如果只有 INSERT 和 SELECT 操作，可以选择Archive 引擎，Archive 存储引擎支持高并发的插入操作，但是本身并不是事务安全的。Archive 存储引擎非常适合存储归档数据，**如记录日志信息可以使用 Archive 引擎。**

