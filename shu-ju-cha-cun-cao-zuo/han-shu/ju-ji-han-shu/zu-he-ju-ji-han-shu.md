# 组合聚集函数

目前为止的所有聚集函数例子都只涉及单个函数。但实际上SELECT 语句可根据需要包含多个聚集函数。请看下面的例子：

```text
SELECT COUNT(*) AS num_items,
       MIN(prod_price) AS price_min,
       MAX(prod_price) AS price_max,
       AVG(prod_price) AS price_avg
FROM products;
```

![](../../../.gitbook/assets/image%20%28123%29.png)

