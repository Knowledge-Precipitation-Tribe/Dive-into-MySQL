# 修改存储过程

在实际开发过程中，业务需求修改的情况时有发生，所以修改 MySQL 中的存储过程是不可避免的。

 MySQL 中通过 ALTER PROCEDURE 语句来修改存储过程。本节将详细讲解修改存储过程的方法。

 MySQL 中修改存储过程的语法格式如下：

```text
ALTER PROCEDURE 存储过程名 [ 特征 ... ]
```

`特征`指定了存储过程的特性，可能的取值有：

*  CONTAINS SQL 表示子程序包含 SQL 语句，但不包含读或写数据的语句。
*  NO SQL 表示子程序中不包含 SQL 语句。
*  READS SQL DATA 表示子程序中包含读数据的语句。
*  MODIFIES SQL DATA 表示子程序中包含写数据的语句。
*  SQL SECURITY { DEFINER \|INVOKER } 指明谁有权限来执行。
*  DEFINER 表示只有定义者自己才能够执行。
*  INVOKER 表示调用者可以执行。
*  COMMENT 'string' 表示注释信息。

##  实例 1

 下面修改存储过程 showstuscore 的定义，将读写权限改为 MODIFIES SQL DATA，并指明调用者可以执行，代码如下：

```text
mysql> ALTER PROCEDURE showstuscore MODIFIES SQL DATA SQL SECURITY INVOKER;
Query OK, 0 rows affected (0.01 sec)
```

 执行代码，并查看修改后的信息，运行结果如下：

```text
mysql> SHOW CREATE PROCEDURE showstuscore \G
*************************** 1. row ***************************
           Procedure: showstuscore
            sql_mode: STRICT_TRANS_TABLES,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
    Create Procedure: CREATE DEFINER=`root`@`localhost` PROCEDURE `showstuscore`()
    MODIFIES SQL DATA
    SQL SECURITY INVOKER
BEGIN
SELECT id,name,score FROM studentinfo;
END
character_set_client: gbk
collation_connection: gbk_chinese_ci
  Database Collation: latin1_swedish_ci
1 row in set (0.00 sec)
```

 结果显示，存储过程修改成功。从运行结果可以看到，访问数据的权限已经变成了 MODIFIES SQL DATA，安全类型也变成了 INVOKE。

 提示：ALTER PROCEDURE 语句用于修改存储过程的某些特征。如果要修改存储过程的内容，可以先删除原存储过程，再以相同的命名创建新的存储过程；如果要修改存储过程的名称，可以先删除原存储过程，再以不同的命名创建新的存储过程。

