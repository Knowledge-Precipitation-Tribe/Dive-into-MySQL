# COUNT函数

COUNT\(\)函数进行计数。可利用COUNT\(\)确定表中行的数目或符合特 定条件的行的数目。

COUNT\(\)函数有两种使用方式。

* 使用COUNT\(\*\)对表中行的数目进行计数，不管表列中包含的是空值（NULL）还是非空值。
* 使用 COUNT\(column\) 对特定列中具有值的行进行计数， 忽略NULL值。

下面的例子返回customers表中客户的总数：

```text
SELECT COUNT(*) AS num_cust
FROM customers;
```

![](../../../.gitbook/assets/image%20%2854%29.png)

下面的例子只对具有电子邮件地址的客户计数：

```text
SELECT COUNT(cust_email) AS num_cust
FROM customers;
```

![](../../../.gitbook/assets/image%20%2888%29.png)

