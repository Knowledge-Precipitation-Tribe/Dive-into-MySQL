# 事务隔离级别

SQL 标准定义了四个隔离级别：

* **READ-UNCOMMITTED\(读取未提交\)：** 最低的隔离级别，允许读取尚未提交的数据变更，**可能会导致脏读、幻读或不可重复读**。
* **READ-COMMITTED\(读取已提交\)：** 允许读取并发事务已经提交的数据，**可以阻止脏读，但是幻读或不可重复读仍有可能发生**。
* **REPEATABLE-READ\(可重复读\)：** 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，**可以阻止脏读和不可重复读，但幻读仍有可能发生**。
* **SERIALIZABLE\(可串行化\)：** 最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，**该级别可以防止脏读、不可重复读以及幻读**。

| 隔离级别 | 脏读 | 不可重复读 | 幻读 |
| :--- | :--- | :--- | :--- |
| READ-UNCOMMITTED | √ | √ | √ |
| READ-COMMITTED | × | √ | √ |
| REPEATABLE-READ | × | × | √ |
| SERIALIZABLE | × | × | × |

MySQL InnoDB 存储引擎的默认支持的隔离级别是 **REPEATABLE-READ（可重读）**。我们可以通过`SELECT @@tx_isolation;`命令来查看,MySQL 8.0 该命令改为`SELECT @@transaction_isolation;`

![](../../.gitbook/assets/image%20%283%29.png)

这里需要注意的是：与SQL标准不同的地方在于InnoDB存储引擎在REPEATABLE-READ（可重读）**事务隔离级别下使用的是**[**Next-Key**](../../shu-ju-biao-cao-zuo/bing-fa-kong-zhi/nextkey-suo.md) **Lock锁算法，因此可以避免幻读的产生，这与其他数据库系统\(如 SQL Server\)是不同的。所以说InnoDB存储引擎的默认支持的隔离级别是 REPEATABLE-READ（可重读）** 已经可以完全保证事务的隔离性要求，即达到了SQL标准的SERIALIZABLE\(可串行化\)隔离级别。

因为隔离级别越低，事务请求的锁越少，所以大部分数据库系统的隔离级别都是**READ-COMMITTED\(读取提交内容\):**，但是你要知道的是InnoDB存储引擎默认使用**REPEATABLE-READ（可重读）**并不会有任何性能损失。

InnoDB存储引擎在 **分布式事务** 的情况下一般会用到**SERIALIZABLE\(可串行化\)**隔离级别。

## 锁问题

通过加锁解决问题请见：[并发控制](../../shu-ju-biao-cao-zuo/bing-fa-kong-zhi/)

