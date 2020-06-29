# 第n高的薪水

## SQL架构

```sql
Create table If Not Exists Employee (Id int, Salary int)
Truncate table Employee
insert into Employee (Id, Salary) values ('1', '100')
insert into Employee (Id, Salary) values ('2', '200')
insert into Employee (Id, Salary) values ('3', '300')
```

## 题目描述

编写一个 SQL 查询，获取 Employee 表中第n高的薪水（Salary） 。

![](../../.gitbook/assets/image%20%28138%29.png)

例如上述 `Employee` 表，_n = 2_ 时，应返回第二高的薪水 `200`。如果不存在第 _n_ 高的薪水，那么查询应返回 `null`。

![](../../.gitbook/assets/image%20%28139%29.png)

{% hint style="info" %}
来源：力扣（LeetCode） 链接：[https://leetcode-cn.com/problems/nth-highest-salary/](https://leetcode-cn.com/problems/nth-highest-salary/) 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{% endhint %}

## 题解

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
      # Write your MySQL query statement below.
      SELECT 
          DISTINCT salary 
      FROM 
          (SELECT 
                salary, @r:=IF(@p=salary, @r, @r+1) AS rnk,  @p:= salary 
            FROM  
                employee, (SELECT @r:=0, @p:=NULL)init 
            ORDER BY 
                salary DESC) tmp
      WHERE rnk = N
  );
END
```

{% hint style="info" %}
作者：luanhz 链接：[https://leetcode-cn.com/problems/nth-highest-salary/solution/mysql-zi-ding-yi-bian-liang-by-luanz/](https://leetcode-cn.com/problems/nth-highest-salary/solution/mysql-zi-ding-yi-bian-liang-by-luanz/) 来源：力扣（LeetCode） 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
{% endhint %}

