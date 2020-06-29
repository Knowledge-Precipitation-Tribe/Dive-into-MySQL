# 组合两个表

## SQL架构

```sql
Create table Person (PersonId int, FirstName varchar(255), LastName varchar(255))
Create table Address (AddressId int, PersonId int, City varchar(255), State varchar(255))
Truncate table Person
insert into Person (PersonId, LastName, FirstName) values ('1', 'Wang', 'Allen')
Truncate table Address
insert into Address (AddressId, PersonId, City, State) values ('1', '2', 'New York City', 'New York')
```

## 题目描述

表1: Person

![](../../.gitbook/assets/image%20%28137%29.png)

表2: Address

![](../../.gitbook/assets/image%20%28136%29.png)

编写一个 SQL 查询，满足条件：无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息：

`FirstName, LastName, City, State`

{% hint style="info" %}
来源：力扣（LeetCode） 链接：[https://leetcode-cn.com/problems/combine-two-tables](https://leetcode-cn.com/problems/combine-two-tables) 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{% endhint %}

## 题解

```sql
select FirstName, LastName, City, State
from Person left join Address
on Person.PersonId = Address.PersonId
```

