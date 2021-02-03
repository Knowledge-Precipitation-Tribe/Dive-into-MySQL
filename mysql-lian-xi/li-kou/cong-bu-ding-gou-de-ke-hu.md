# 从不订购的客户

## SQL架构

```sql
Create table If Not Exists Customers (Id int, Name varchar(255))
Create table If Not Exists Orders (Id int, CustomerId int)
Truncate table Customers
insert into Customers (Id, Name) values ('1', 'Joe')
insert into Customers (Id, Name) values ('2', 'Henry')
insert into Customers (Id, Name) values ('3', 'Sam')
insert into Customers (Id, Name) values ('4', 'Max')
Truncate table Orders
insert into Orders (Id, CustomerId) values ('1', '3')
insert into Orders (Id, CustomerId) values ('2', '1')
```

## 题目描述

某网站包含两个表，Customers 表和 Orders 表。编写一个 SQL 查询，找出所有从不订购任何东西的客户。

Customers 表：

![](../../.gitbook/assets/image%20%28156%29.png)

Orders 表：

![](../../.gitbook/assets/image%20%28158%29.png)

例如给定上述表格，你的查询应返回：

![](../../.gitbook/assets/image%20%28157%29.png)

{% hint style="info" %}
来源：力扣（LeetCode） 链接：[https://leetcode-cn.com/problems/customers-who-never-order](https://leetcode-cn.com/problems/customers-who-never-order) 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{% endhint %}

## 题解

```sql
select Name as Customers from Customers where id not in (select CustomerId from Orders)
```

