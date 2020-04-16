# 图解MySQL内连接、外连接、左连接、右连接

来源：plg17:[https://blog.csdn.net/plg17/article/details/78758593](https://blog.csdn.net/plg17/article/details/78758593) 

 用两个表（a\_table、b\_table），关联字段a\_table.a\_id和b\_table.b\_id来演示一下MySQL的内连接、外连接（ 左\(外\)连接、右\(外\)连接、全\(外\)连接）。

数据库表：a\_table、b\_table

主题：内连接、左连接（左外连接）、右连接（右外连接）、全连接（全外连接）

## 前提

### **建表语句：**

```text
CREATE TABLE `a_table` (
  `a_id` int(11) DEFAULT NULL,
  `a_name` varchar(10) DEFAULT NULL,
  `a_part` varchar(10) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

```text
CREATE TABLE `b_table` (
  `b_id` int(11) DEFAULT NULL,
  `b_name` varchar(10) DEFAULT NULL,
  `b_part` varchar(10) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

### 表测试数据：

![](https://img-blog.csdn.net/20171209135012639?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGxnMTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

## 一、内连接

 关键字：inner join on

```text
select * from a_table a inner join b_table b on a.a_id = b.b_id;
```

执行结果：

![](https://img-blog.csdn.net/20171209133941291?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGxnMTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

 说明：组合两个表中的记录，返回关联字段相符的记录，也就是返回两个表的交集（阴影）部分。

![](https://img-blog.csdn.net/20171209135846780?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGxnMTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 二、左连接（左外连接）

关键字：left join on / left outer join on

```text
select * from a_table a left join b_table b on a.a_id = b.b_id;
```

执行结果：

![](https://img-blog.csdn.net/20171209141445680?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGxnMTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

说明：

left join 是left outer join的简写，它的全称是左外连接，是外连接中的一种。

左\(外\)连接，左表\(a\_table\)的记录将会全部表示出来，而右表\(b\_table\)只会显示符合搜索条件的记录。右表记录不足的地方均为NULL。  


![](https://img-blog.csdn.net/20171209142610819?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGxnMTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 三、右连接（右外连接）

关键字：right join on / right outer join on

```text
select * from a_table a right outer join b_table b on a.a_id = b.b_id;
```

执行结果：

![](https://img-blog.csdn.net/20171209143426953?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGxnMTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

说明：

right join是right outer join的简写，它的全称是右外连接，是外连接中的一种。  


与左\(外\)连接相反，右\(外\)连接，左表\(a\_table\)只会显示符合搜索条件的记录，而右表\(b\_table\)的记录将会全部表示出来。左表记录不足的地方均为NULL。

![](https://img-blog.csdn.net/20171209144056668?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcGxnMTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 四、全连接（全外连接）

MySQL目前不支持此种方式，可以用其他方式替代解决。

## 五、补充，MySQL如何执行关联查询

MySQL认为任何一个查询都是一次“关联”，并不仅仅是一个查询需要到两个表匹配才叫关联，所以在MySQL中，每一个查询，每一个片段（包括子查询，甚至基于单表查询）都可以是一次关联。

当前MySQL关联执行的策略很简单：MySQL对任何关联都执行嵌套循环关联操作，即MySQL先在一个表中循环取出单条数据，然后在嵌套循环到下一个表中寻找匹配的行，依次下去，直到找到所有表中匹配的行为止。然后根据各个表匹配的行，返回查询中需要的各个列。请看下面的例子中的简单的查询：

```text
select tbl1.col1, tbl2.col2 from tbl1 inner join tbl2 using(col3) where tbl1.col1 in (5, 6);
```

假设MySQL按照查询中的表顺序进行关联操作，我们则可以用下面的伪代码表示MySQL将如何完成这个查询：

```text
outer_iter = iterator over tbl1 where col1 in (5, 6)
outer_row = outer_iter.next
while outer_row
    inner_iter = iterator over tbl2 where col3 = outer_row.col3
    inner_row = inner_iter.next
    while inner_row
        output [ outer_row.col1, inner_row.col2]
        inner_row = inner_iter.next
    end
    outer_row = outer_iter.next
end
```

上面的执行计划对于单表查询和多表关联查询都适用，如果是一个单表查询，那么只需要上面外层的基本操作。对于外连接，上面的执行过程仍然适用。例如，我们将上面的查询语句修改如下：  
 select tbl1.col1, tbl2.col2 from tbl1 left outer join tbl2 using\(col3\) where tbl1.col1 in \(5, 6\);

那么，对应的伪代码如下：

```text
outer_iter = iterator over tbl1 where col1 in (5, 6)
outer_row = outer_iter.next
while outer_row
    inner_iter = iterator over tbl2 where col3 = outer_row.col3
    inner_row = inner_iter.next
    if inner_row
        while inner_row
            output [ outer_row.col1, inner_row.col2]
            inner_row = inner_iter.next
        end
    else
        output [ outer_row.col1, null]
    end
        outer_row = outer_iter.next
end
```

**说明：第五部分摘自《高性能MySQL 第三版》**

