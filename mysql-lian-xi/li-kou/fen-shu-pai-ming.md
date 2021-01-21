# 分数排名

## SQL架构

```sql
Create table If Not Exists Scores (Id int, Score DECIMAL(3,2))
Truncate table Scores
insert into Scores (Id, Score) values ('1', '3.5')
insert into Scores (Id, Score) values ('2', '3.65')
insert into Scores (Id, Score) values ('3', '4.0')
insert into Scores (Id, Score) values ('4', '3.85')
insert into Scores (Id, Score) values ('5', '4.0')
insert into Scores (Id, Score) values ('6', '3.65')
```

## 题目描述

编写一个 SQL 查询来实现分数排名。

如果两个分数相同，则两个分数排名（Rank）相同。请注意，平分后的下一个名次应该是下一个连续的整数值。换句话说，名次之间不应该有“间隔”。

![](../../.gitbook/assets/image%20%28143%29.png)

例如，根据上述给定的 Scores 表，你的查询应该返回（按分数从高到低排列）： 

![](../../.gitbook/assets/image%20%28142%29.png)

重要提示：对于 MySQL 解决方案，如果要转义用作列名的保留字，可以在关键字之前和之后使用撇号。例如 `Rank`

{% hint style="info" %}
来源：力扣（LeetCode） 链接：[https://leetcode-cn.com/problems/rank-scores](https://leetcode-cn.com/problems/rank-scores) 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{% endhint %}

## 题解

```sql
SELECT Score, dense_rank() over (ORDER BY Score DESC) AS `Rank`
FROM Scores
```

{% embed url="https://leetcode-cn.com/problems/rank-scores/solution/tu-jie-sqlmian-shi-ti-jing-dian-pai-ming-wen-ti-by/" %}

