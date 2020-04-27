# 删除存储过程

存储过程被创建后，就会一直保存在数据库服务器上，直至被删除。当 MySQL 数据库中存在废弃的存储过程时，我们需要将它从数据库中删除。

 MySQL 中使用 DROP PROCEDURE 语句来删除数据库中已经存在的存储过程。语法格式如下：

```text
DROP { PROCEDURE | FUNCTION } [ IF EXISTS ] <过程名>
```

 语法说明如下：

*  过程名：指定要删除的存储过程的名称。
*  IF EXISTS：指定这个关键字，用于防止因删除不存在的存储过程而引发的错误。

{% hint style="info" %}
注意：存储过程名称后面没有参数列表，也没有括号，在删除之前，必须确认该存储过程没有任何依赖关系，否则会导致其他与之关联的存储过程无法运行。
{% endhint %}

##  实例 1

 下面删除存储过程 showstuscore，SQL 语句和运行结果如下：

```text
mysql> DROP PROCEDURE showstuscore;
Query OK, 0 rows affected (0.08 sec)
```

 删除后，可以通过查询 information\_schema 数据库下的 routines 表来确认上面的删除是否成功。SQL 语句和运行结果如下：

```text
mysql> SELECT * FROM information_schema.routines WHERE routine_name='showstuscore';
Empty set (0.03 sec)
```

 结果显示，没有查询出任何记录，说明存储过程 showstuscore 已经被删除了。  


