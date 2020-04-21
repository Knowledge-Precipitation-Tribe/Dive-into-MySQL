# 并发事务带来的问题

在典型的应用程序中，多个事务并发运行，经常会操作相同的数据来完成各自的任务（多个用户对统一数据进行操作）。并发虽然是必须的，但可能会导致以下的问题。

我们先来查看一下数据库的[隔离级别](shi-wu-ge-li-ji-bie.md)

![](../../.gitbook/assets/image%20%283%29.png)

然后我们创建一个数据表

```text
CREATE TABLE ttd(id INT);
```

## **脏读（Dirty read）**

当一个事务正在访问数据并且对数据进行了修改，而这种修改还没有提交到数据库中，这时另外一个事务也访问了这个数据，然后使用了这个数据。因为这个数据是还没有提交的数据，那么另外一个事务读到的这个数据是“脏数据”，依据“脏数据”所做的操作可能是不正确的。

{% code title="进程1" %}
```text
mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into ttd values(1);
Query OK, 1 row affected (0.00 sec)
```
{% endcode %}

这时在RR的隔离级别下，在进程2是不能读取到数据的

{% code title="进程2" %}
```text
mysql> select * from ttd;
Empty set (0.00 sec)
```
{% endcode %}

在进程2中修改隔离级别

```text
mysql> set session transaction isolation level read uncommitted;
Query OK, 0 rows affected (0.00 sec)
```

这时我们在进程1中的事务仍没有提交，但是在进程2中却读到了数据，就出现了脏读的情况

```text
mysql> select * from ttd;
+------+
| id   |
+------+
|    1 |
+------+
1 row in set (0.00 sec)
```

## **丢失修改（Lost to modify）**

指在一个事务读取一个数据时，另外一个事务也访问了该数据，那么在第一个事务中修改了这个数据后，第二个事务也修改了这个数据。这样第一个事务内的修改结果就被丢失，因此称为丢失修改。 例如：事务1读取某表中的数据A=20，事务2也读取A=20，事务1修改A=A-1，事务2也修改A=A-1，最终结果A=19，事务1的修改被丢失。

## **不可重复读（Unrepeatableread）**

指在一个事务内多次读同一数据。在这个事务还没有结束时，另一个事务也访问该数据。那么，在第一个事务中的两次读数据之间，由于第二个事务的修改导致第一个事务两次读取的数据可能不太一样。这就发生了在一个事务内两次读到的数据是不一样的情况，因此称为不可重复读。

我们先修改一下事务的隔离级别

```text
mysql> set session transaction isolation level read committed;
Query OK, 0 rows affected (0.00 sec)
```

我们先在进程1中查询数据

{% code title="进程1" %}
```text
mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from ttd;
+------+
| id   |
+------+
|    1 |
+------+
1 row in set (0.00 sec)
```
{% endcode %}

这时我们在进程2中开启事务并修改数据

{% code title="进程2" %}
```text
mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> update ttd set id = 2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> commit;
Query OK, 0 rows affected (0.01 sec)
```
{% endcode %}

这时我们在进程1中再次查询数据就会发生不可重复读取现象。

{% code title="进程1" %}
```text
mysql> select * from ttd;
+------+
| id   |
+------+
|    2 |
+------+
1 row in set (0.00 sec)
```
{% endcode %}

## **幻读（Phantom read）**

幻读与不可重复读类似。它发生在一个事务（T1）读取了几行数据，接着另一个并发事务（T2）插入了一些数据时。在随后的查询中，第一个事务（T1）就会发现多了一些原本不存在的记录，就好像发生了幻觉一样，所以称为幻读。

首先修改事务隔离级别

```text
mysql> set session transaction isolation level repeatable read;
Query OK, 0 rows affected (0.00 sec)
```

首先在进程1中开启事务并执行查询操作

{% code title="进程1" %}
```text
mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from ttd;
+------+
| id   |
+------+
|    3 |
+------+
1 row in set (0.00 sec)
```
{% endcode %}

这时开启第二个进程，开启事务并且插入数据

{% code title="进程2" %}
```text
ysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into ttd values(5);
Query OK, 1 row affected (0.00 sec)

mysql> commit;
Query OK, 0 rows affected (0.00 sec)
```
{% endcode %}

这时在进程1中再执行查询操作会发现出现了幻读情况

```text
mysql> select * from ttd;
+------+
| id   |
+------+
|    3 |
|    5 |
+------+
2 row in set (0.00 sec)
```

{% hint style="info" %}
注意在InnoDB引擎下，RR级别的事务隔离已经解决了幻读问题，使用的是[Next-key](../../shu-ju-biao-cao-zuo/bing-fa-kong-zhi/nextkey-suo.md)锁。
{% endhint %}

## **不可重复度和幻读区别**

不可重复读的重点是修改，幻读的重点在于新增或者删除。

例1（同样的条件, 你读取过的数据, 再次读取出来发现值不一样了 ）：事务1中的A先生读取自己的工资为 1000的操作还没完成，事务2中的B先生就修改了A的工资为2000，导致A再读自己的工资时工资变为 2000；这就是不可重复读。

例2（同样的条件, 第1次和第2次读出来的记录数不一样 ）：假某工资单表中工资大于3000的有4人，事务1读取了所有工资大于3000的人，共查到4条记录，这时事务2又插入了一条工资大于3000的记录，事务1再次读取时查到的记录就变为了5条，这样就导致了幻读。

