# 聚集不同值

以上5个聚集函数都可以如下使用：

* 对所有的行执行计算，指定ALL参数或不给参数（因为ALL是默认 行为）；  
* 只包含不同的值，指定DISTINCT参数。

下面的例子使用AVG\(\)函数返回特定供应商提供的产品的平均价格。 它与上面的SELECT语句相同，但使用了DISTINCT参数，因此平均值只考虑各个不同的价格：

```text
SELECT AVG(DISTINCT prod_price) AS avg_price
FROM products
WHERE vend_id = 1003;
```

![](../../../.gitbook/assets/image%20%2874%29.png)

