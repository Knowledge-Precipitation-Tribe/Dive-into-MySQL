# 执行算数计算

计算字段的另一常见用途是对检索出的数据进行算术计算。举一个例子，orders表包含收到的所有订单，orderitems表包含每个订单中的各项物品。下面的SQL语句检索订单号20005中的所有物品：

```text
SELECT prod_id, quantity, item_price
FROM orderitems
WHERE order_num = 20005;
```



![](../../.gitbook/assets/image%20%2849%29.png)

item\_price列包含订单中每项物品的单价。如下汇总物品的价格（单价乘以订购数量）：

```text
SELECT prod_id, quantity, item_price, quantity*item_price AS expanded_price
FROM orderitems
WHERE order_num = 20005;
```

![](../../.gitbook/assets/image%20%2819%29.png)

