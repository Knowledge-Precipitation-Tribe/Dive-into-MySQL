# 自定义函数

在使用 MySQL 的过程中，MySQL 自带的函数可能完成不了我们的业务需求，这时候就需要自定义函数。

自定义函数是一种与存储过程十分相似的过程式数据库对象。它与存储过程一样，都是由 SQL 语句和过程式语句组成的代码片段，并且可以被应用程序和其他 SQL 语句调用。

自定义函数与存储过程之间存在几点区别：

* 自定义函数不能拥有输出参数，这是因为自定义函数自身就是输出参数；而存储过程可以拥有输出参数。
* 自定义函数中必须包含一条 RETURN 语句，而这条特殊的 SQL 语句不允许包含于存储过程中。
* 可以直接对自定义函数进行调用而不需要使用 CALL 语句，而对存储过程的调用需要使用 CALL 语句。

## 创建并使用自定义函数

可以使用 CREATE FUNCTION 语句创建自定义函数。

语法格式如下：

```text
CREATE FUNCTION <函数名> ( [ <参数1> <类型1> [ , <参数2> <类型2>] ] … )
   RETURNS <类型>
   <函数主体>
```

 语法说明如下：

*  `<函数名>`：指定自定义函数的名称。注意，自定义函数不能与存储过程具有相同的名称。
*  `<参数><类型>`：用于指定自定义函数的参数。这里的参数只有名称和类型，不能指定关键字 IN、OUT 和 INOUT。
*  `RETURNS<类型>`：用于声明自定义函数返回值的数据类型。其中，`<类型>`用于指定返回值的数据类型。
*  `<函数主体>`：自定义函数的主体部分，也称函数体。所有在存储过程中使用的 SQL 语句在自定义函数中同样适用，包括前面所介绍的局部变量、SET 语句、流程控制语句、游标等。除此之外，自定义函数体还必须包含一个 `RETURN<值>` 语句，其中`<值>`用于指定自定义函数的返回值。

在 RETURN VALUE 语句中包含 SELECT 语句时，SELECT 语句的返回结果只能是一行且只能有一列值。

若要查看数据库中存在哪些自定义函数，可以使用 SHOW FUNCTION STATUS 语句；若要查看数据库中某个具体的自定义函数，可以使用 SHOW CREATE FUNCTION&lt;函数名&gt; 语句，其中`<函数名>`用于指定该自定义函数的名称。

【实例 1】创建存储函数，名称为StuNameById，该函数返回SELECT语句的查询结果，数值类型为字符串类型，输入的SQL语句和执行结果如下所示。

```text
mysql> CREATE FUNCTION StuNameById()
    -> RETURNS VARCHAR(45)
    -> RETURN
    -> (SELECT name FROM tb_students_info
    -> WHERE id=1);
Query OK， 0 rows affected (0.09 sec)
```

> 注意：当使用 DELIMITER 命令时，应该避免使用反斜杠“\”字符，因为反斜杠是 MySQL 的转义字符。

成功创建自定义函数后，就可以如同调用系统内置函数一样，使用关键字 SELECT 调用用户自定义的函数，语法格式为：

```text
SELECT <自定义函数名> ([<参数> [,...]])
```

【实例 2】调用自定义函数StuNameById，查看函数的运行结果，如下所示。

```text
mysql> SELECT StuNameById();
+---------------+
| StuNameById() |
+---------------+
| Dany          |
+---------------+
1 row in set (0.24 sec)
```

## 修改自定义函数

可以使用 ALTER FUNCTION 语句来修改自定义函数的某些相关特征。若要修改自定义函数的内容，则需要先删除该自定义函数，然后重新创建。

## 删除自定义函数

自定义函数被创建后，一直保存在数据库服务器上以供使用，直至被删除。删除自定义函数的方法与删除存储过程的方法基本一样，可以使用DROP FUNCTION语句来实现。

语法格式如下：

```text
DROP FUNCTION [ IF EXISTS ] <自定义函数名>
```

 语法说明如下。  
 `<自定义函数名>`：指定要删除的自定义函数的名称。  
 `IF EXISTS`：指定关键字，用于防止因误删除不存在的自定义函数而引发错误。

【实例 3】删除自定义函数StuNameById，查看函数的运行结果，如下所示。

```text
mysql> DROP FUNCTION StuNameById;
Query OK, 0 rows affected (0.09 sec)
mysql> SELECT StuNameById();
ERROR 1305 (42000): FUNCTION test_db.StuNameById does not exist
```

