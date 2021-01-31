# 查找重复的电子邮箱

## SQL架构

```sql
Create table If Not Exists Person (Id int, Email varchar(255))
Truncate table Person
insert into Person (Id, Email) values ('1', 'a@b.com')
insert into Person (Id, Email) values ('2', 'c@d.com')
insert into Person (Id, Email) values ('3', 'a@b.com')
```

## 题目描述

编写一个 SQL 查询，查找 Person 表中所有重复的电子邮箱。

示例：

![](../../.gitbook/assets/image%20%28155%29.png)

根据以上输入，你的查询应返回以下结果：

![](../../.gitbook/assets/image%20%28154%29.png)

说明：所有电子邮箱都是小写字母。

{% hint style="info" %}
来源：力扣（LeetCode） 链接：[https://leetcode-cn.com/problems/duplicate-emails](https://leetcode-cn.com/problems/duplicate-emails) 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
{% endhint %}

## 题解

```sql
select Email
from person 
group by email
having count(1)>1
```

