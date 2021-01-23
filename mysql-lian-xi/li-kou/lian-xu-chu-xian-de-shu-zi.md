# 连续出现的数字

## SQL架构

```sql
Create table If Not Exists Logs (Id int, Num int)
Truncate table Logs
insert into Logs (Id, Num) values ('1', '1')
insert into Logs (Id, Num) values ('2', '1')
insert into Logs (Id, Num) values ('3', '1')
insert into Logs (Id, Num) values ('4', '2')
insert into Logs (Id, Num) values ('5', '1')
insert into Logs (Id, Num) values ('6', '2')
insert into Logs (Id, Num) values ('7', '2')
```

题目描述

编写一个 SQL 查询，查找所有至少连续出现三次的数字。

![](../../.gitbook/assets/image%20%28150%29.png)

例如，给定上面的 Logs 表， 1 是唯一连续出现至少三次的数字。

![](../../.gitbook/assets/image%20%28144%29.png)

{% hint style="info" %}
来源：力扣（LeetCode） 链接：[https://leetcode-cn.com/problems/consecutive-numbers](https://leetcode-cn.com/problems/consecutive-numbers) 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{% endhint %}

## 题解

```sql
SELECT DISTINCT
    l1.Num AS ConsecutiveNums
FROM
    Logs l1,
    Logs l2,
    Logs l3
WHERE
    l1.Id = l2.Id - 1
    AND l2.Id = l3.Id - 1
    AND l1.Num = l2.Num
    AND l2.Num = l3.Num
;
```

{% hint style="info" %}
作者：LeetCode 链接：[https://leetcode-cn.com/problems/consecutive-numbers/solution/lian-xu-chu-xian-de-shu-zi-by-leetcode/](https://leetcode-cn.com/problems/consecutive-numbers/solution/lian-xu-chu-xian-de-shu-zi-by-leetcode/) 来源：力扣（LeetCode） 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
{% endhint %}

