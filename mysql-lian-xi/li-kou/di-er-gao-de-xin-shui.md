# 第二高的薪水

## SQL架构

```sql
Create table If Not Exists Employee (Id int, Salary int)
Truncate table Employee
insert into Employee (Id, Salary) values ('1', '100')
insert into Employee (Id, Salary) values ('2', '200')
insert into Employee (Id, Salary) values ('3', '300')
```

## 题目描述

编写一个 SQL 查询，获取 Employee 表中第二高的薪水（Salary） 。

![](../../.gitbook/assets/image%20%28138%29.png)

例如上述 Employee 表，SQL查询应该返回 200 作为第二高的薪水。如果不存在第二高的薪水，那么查询应返回 null。

![](../../.gitbook/assets/image%20%28139%29.png)

{% hint style="info" %}
来源：力扣（LeetCode） 链接：[https://leetcode-cn.com/problems/second-highest-salary](https://leetcode-cn.com/problems/second-highest-salary) 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{% endhint %}

## 题解

```sql
SELECT
    IFNULL(
      (SELECT DISTINCT Salary
       FROM Employee
       ORDER BY Salary DESC
        LIMIT 1 OFFSET 1),
    NULL) AS SecondHighestSalary
```

