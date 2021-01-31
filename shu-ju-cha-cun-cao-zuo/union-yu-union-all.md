# union与union all

**Union因为要进行重复值扫描，所以效率低。如果合并没有刻意要删除重复行，那么就使用Union All，两个要联合的SQL语句字段个数必须一样，而且字段类型要“相容”（一致）；**

如果我们需要将两个select语句的结果作为一个整体显示出来，我们就需要用到union或者union all关键字。union\(或称为联合\)的作用是将多个结果合并在一起显示出来。

union和union all的区别

* union会自动压缩多个结果集合中的重复结果，对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序。
* union all则将所有的结果全部显示出来，不管是不是重复。对两个结果集进行并集操作，包括重复行，不进行排序；
* Intersect：对两个结果集进行交集操作，不包括重复行，同时进行默认规则的排序；
* Minus：对两个结果集进行差操作，不包括重复行，同时进行默认规则的排序。

例如：

```sql
select employee_id,job_id from employees
union
select employee_id,job_id from job_history
```

以上将两个表的结果联合在一起。这两个例子会将两个select语句的结果中的重复值进行压缩，也就是结果的数据并不是两条结果的条数的和。如果希望即使重复的结果显示出来可以使用union all。

