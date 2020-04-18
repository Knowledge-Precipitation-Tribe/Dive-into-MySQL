# SUM函数

SUM\(\)用来返回指定列值的和（总计）。

下面举一个例子，orderitems表包含订单中实际的物品，每个物品有相应的数量（ quantity ）。 可如下检索所订购物品的总数（所有 quantity值之和）：

```text
SELECT SUM(quantity) AS item_ordered
FROM orderitems
WHERE order_num = 20005;
```

![](../../../.gitbook/assets/image%20%281%29.png)

SUM\(\)也可以用来合计计算值。在下面的例子中，合计每项物品的 item\_price\*quantity，得出总的订单金额：

```text
SELECT SUM(item_price*quantity) AS total_price
FROM orderitems
WHERE order_num = 20005;
```

