# 创建数据表

在MySQL中使用\`CREATE TABLE\`语句创建表。语法格式为：

```text
CREATE TABLE <表名> (<列名1><类型>, <列名2><类型>, ...)
```

{% hint style="info" %}
要创建的表的名称不区分大小写，不能使用SQL语言中的关键字，如DROP、ALTER、INSERT等。
{% endhint %}

数据表属于数据库，在创建数据表之前，应使用语句“USE&lt;数据库&gt;”指定操作在哪个数据库中进行，如果没有选择数据库，就会抛出 No database selected 的错误。

### 案例

创建员工表 tb\_emp1，结构如下表所示。

![](../.gitbook/assets/image%20%2820%29.png)



