# AVG函数

AVG\(\)通过对表中行数计数并计算特定列值之和，求得该列的平均值。AVG\(\)可用来返回所有列的平均值，也可以用来返回特定列或行的平 均值。

下面的例子使用AVG\(\)返回products表中所有产品的平均价格：

```text
SELECT AVG(prod_price) AS avg_price
FROM products;
```

![](../../../.gitbook/assets/image%20%2820%29.png)

AVG\(\)也可以用来确定特定列或行的平均值。下面的例子返回特定供应商所提供产品的平均价格：

```text
SELECT AVG(prod_price) AS avg_price
FROM products;
WHERE vend_id = 1003;
```

![](../../../.gitbook/assets/image%20%2838%29.png)

