# 拼接字段

为了说明如何使用计算字段，举一个创建由两列组成的标题的简单例子。

vendors表包含供应商名和位置信息。假如要生成一个供应商报表， 需要在供应商的名字中按照name\(location\)这样的格式列出供应商的位置。

此报表需要单个值， 而表中数据存储在两个列vend_name和 vend_ country中。此外，需要用括号将vend\_country括起来，这些东西都没有明确存储在数据库表中。 我们来看看怎样编写返回供应商名和位置的 SELECT语句。

{% hint style="info" %}
拼接（concatenate） 将值联结到一起构成单个值。
{% endhint %}

解决办法是把两个列拼接起来。在MySQL的SELECT语句中，可使用 Concat\(\)函数来拼接两个列。

```text
SELECT Concat(vend_name, '(',vend_country ,')')
FROM vendors
ORDER BY vend_name;
```

![](../../.gitbook/assets/image%20%2893%29.png)

还可以通过删除数据右侧多余的空格来整理数据，这可以使用MySQL的RTrim\(\)函数来完成，如下所示：

```text
SELECT Concat(RTrim(vend_name), '(', RTrim(vend_country), ')')
FROM vendors
ORDER BY vend_name;
```

## 使用别名

从前面的输出中可以看到，SELECT语句拼接地址字段工作得很好。 但此新计算列的名字是什么呢？实际上它没有名字，它只是一个值。如 果仅在SQL查询工具中查看一下结果，这样没有什么不好。但是，一个未 命名的列不能用于客户机应用中，因为客户端没有办法引用它。

为了解决这个问题，SQL支持列别名。别名（alias）是一个字段或值的替换名。别名用AS关键字赋予。请看下面的SELECT语句：

```text
SELECT Contact(RTrim(vend_name), '(', RTrim(vend_country), ')')
AS vend_title
FROM vendors
ORDER BY vend_name;
```

![](../../.gitbook/assets/image%20%2864%29.png)

