# 创建存储过程

MySQL 存储过程是一些 SQL 语句的集合，比如有的时候我们可能需要一大串的 SQL 语句，或者说在编写 SQL 语句的过程中还需要设置一些变量的值，这个时候我们就完全有必要编写一个存储过程。下面我们来介绍一下如何创建一个存储过程。

##  基本语法

 可以使用 CREATE PROCEDURE 语句创建存储过程。

 语法格式如下：

```text
CREATE PROCEDURE <过程名> ( [过程参数[,…] ] ) <过程体> [过程参数[,…] ] 格式 [ IN | OUT | INOUT ] <参数名> <类型>
```

 语法说明如下：

###  1\) 过程名

存储过程的名称，默认在当前数据库中创建。若需要在特定数据库中创建存储过程，则要在名称前面加上数据库的名称，即db\_name.sp\_name。需要注意的是，名称应当尽量避免选取与MySQL内置函数相同的名称，否则会发生错误。

###  2\) 过程参数

存储过程的参数列表。其中，`<参数名>`为参数名，`<类型>`为参数的类型（可以是任何有效的 MySQL 数据类型）。当有多个参数时，参数列表中彼此间用逗号分隔。存储过程可以没有参数（此时存储过程的名称后仍需加上一对括号），也可以有 1 个或多个参数。

MySQL存储过程支持**三种类型的参数**，即输入参数、输出参数和输入/输出参数，分别用IN、OUT和INOUT 三个关键字标识。其中，**输入参数可以传递给一个存储过程**，**输出参数用于存储过程需要返回一个操作结果的情形**，**而输入/输出参数既可以充当输入参数也可以充当输出参数**。需要注意的是，参数的取名不要与数据表的列名相同，否则尽管不会返回出错信息，但是存储过程的 SQL 语句会将参数名看作列名，从而引发不可预知的结果。

###  3\) 过程体

存储过程的主体部分，也称为存储过程体，包含在过程调用的时候必须执行的 SQL 语句。这个部分以关键字 BEGIN 开始，以关键字 END 结束。若存储过程体中只有一条 SQL 语句，则可以省略 BEGIN-END 标志。

在存储过程的创建中，经常会用到一个十分重要的 MySQL 命令，即 DELIMITER 命令，特别是对于通过命令行的方式来操作 MySQL 数据库的使用者，更是要学会使用该命令。

在 MySQL 中，服务器处理 SQL 语句默认是以分号作为语句结束标志的。然而，在创建存储过程时，存储过程体可能包含有多条 SQL 语句，这些 SQL 语句如果仍以分号作为语句结束符，那么 MySQL 服务器在处理时会以遇到的第一条 SQL 语句结尾处的分号作为整个程序的结束符，而不再去处理存储过程体中后面的 SQL 语句，这样显然不行。为解决这个问题，通常可使用 DELIMITER 命令将结束命令修改为其他字符。

语法格式如下：

```text
DELIMITER $$
```

 语法说明如下：

*  $$ 是用户定义的结束符，通常这个符号可以是一些特殊的符号，如两个“?”或两个“￥”等。
*  当使用 DELIMITER 命令时，应该避免使用反斜杠“\”字符，因为它是 MySQL 的转义字符。

 在 MySQL 命令行客户端输入如下SQL语句。

```text
mysql > DELIMITER ??
```

 成功执行这条 SQL 语句后，任何命令、语句或程序的结束标志就换为两个问号“??”了。

 若希望换回默认的分号“;”作为结束标志，则在 MySQL 命令行客户端输入下列语句即可：

```text
mysql > DELIMITER ;
```

> 注意：DELIMITER 和分号“;”之间一定要有一个空格。在创建存储过程时，必须具有 CREATE ROUTINE 权限。可以使用 SHOW PROCEDURE STATUS 命令查看数据库中存在哪些存储过程，若要查看某个存储过程的具体信息，则可以使用 SHOW CREATE PROCEDURE &lt;存储过程名&gt;。

##  创建不带参数的存储过程

【实例 1】创建名称为 ShowStuScore 的存储过程，存储过程的作用是从学生成绩信息表中查询学生的成绩信息，输入的 SQL 语句和执行过程如下所示。这里修改结束符号为//。

```text
mysql> DELIMITER //
mysql> CREATE PROCEDURE ShowStuScore()
    -> BEGIN
    -> SELECT * FROM tb_students_score;
    -> END //
Query OK， 0 rows affected (0.09 sec)
```

 创建存储过程 ShowStuScore 后，通过 CALL 语句调用该存储过程的 SQL 语句和执行结果如下所示。

```text
mysql> DELIMITER ;
mysql> CALL ShowStuScore();
+--------------+---------------+
| student_name | student_score |
+--------------+---------------+
| Dany         |            90 |
| Green        |            99 |
| Henry        |            95 |
| Jane         |            98 |
| Jim          |            88 |
| John         |            94 |
| Lily         |           100 |
| Susan        |            96 |
| Thomas       |            93 |
| Tom          |            89 |
+--------------+---------------+
10 rows in set (0.00 sec)
Query OK, 0 rows affected (0.02 sec)
```

##  创建带参数的存储过程

【实例 2】创建名称为 GetScoreByStu 的存储过程，输入参数是学生姓名。存储过程的作用是通过输入的学生姓名从学生成绩信息表中查询指定学生的成绩信息，输入的 SQL 语句和执行过程如下所示。

```text
mysql> DELIMITER //
mysql> CREATE PROCEDURE GetScoreByStu
    -> (IN name VARCHAR(30))
    -> BEGIN
    -> SELECT student_score FROM tb_students_score
    -> WHERE student_name=name;
    -> END //
Query OK, 0 rows affected (0.01 sec)
```

 创建存储过程 GetScoreByStu 后，通过 CALL 语句调用该存储过程的 SQL 语句和执行结果如下所示。

```text
mysql> DELIMITER ;
mysql> CALL GetScoreByStu('Green');
+---------------+
| student_score |
+---------------+
|            99 |
+---------------+
1 row in set (0.03 sec)
Query OK, 0 rows affected (0.03 sec)
```

