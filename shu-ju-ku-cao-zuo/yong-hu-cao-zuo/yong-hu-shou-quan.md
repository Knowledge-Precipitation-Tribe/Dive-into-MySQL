# 用户授权

当成功创建用户账户后，还不能执行任何操作，需要为该用户分配适当的访问权限。可以使用SHOW GRANT FOR语句来查询用户的权限。

> 注意：新创建的用户只有登录MySQL服务器的权限，没有任何其他权限，不能进行其他操作。

 USAGE ON\*.\* 表示该用户对任何数据库和任何表都没有权限。

##  授予用户权限

 对于新建的MySQL用户，必须给它授权，可以用GRANT语句来实现对新建用户的授权。

 语法格式：

```text
GRANT
<权限类型> [ ( <列名> ) ] [ , <权限类型> [ ( <列名> ) ] ]
ON <对象> <权限级别> TO <用户>
其中<用户>的格式：
<用户名> [ IDENTIFIED ] BY [ PASSWORD ] <口令>
[ WITH GRANT OPTION]
| MAX_QUERIES_PER_HOUR <次数>
| MAX_UPDATES_PER_HOUR <次数>
| MAX_CONNECTIONS_PER_HOUR <次数>
| MAX_USER_CONNECTIONS <次数>
```

 语法说明如下：

###  1\) &lt;列名&gt;

可选项。用于指定权限要授予给表中哪些具体的列。

###  2\) ON子句

用于指定权限授予的对象和级别，如在ON关键字后面给出要授予权限的数据库名或表名等。

###  3\) &lt;权限级别&gt;

用于指定权限的级别。可以授予的权限有如下几组：

* 列权限，和表中的一个具体列相关。例如，可以使用UPDATE语句更新表students中student\_name列的值的权限。
* 表权限，和一个具体表中的所有数据相关。例如，可以使用SELECT语句查询表students的所有数据的权限。
* 数据库权限，和一个具体的数据库中的所有表相关。例如，可以在已有的数据库mytest中创建新表的权限。
* 用户权限，和MySQL中所有的数据库相关。例如，可以删除已有的数据库或者创建一个新的数据库的权限。

 对应地，在 GRANT 语句中可用于指定权限级别的值有以下几类格式：

* \*：表示当前数据库中的所有表。
* \*.\*：表示所有数据库中的所有表。
* db\_name.\*：表示某个数据库中的所有表，db\_name指定数据库名。
* db\_name.tbl\_name：表示某个数据库中的某个表或视图，db\_name指定数据库名，tbl\_name指定表名或视图名。
* tbl\_name：表示某个表或视图，tbl\_name 指定表名或视图名。
* db\_name.routine\_name：表示某个数据库中的某个存储过程或函数，routine\_name指定存储过程名或函数名。
* TO子句：用来设定用户口令，以及指定被赋予权限的用户user。若在TO子句中给系统中存在的用户指定口令，则新密码会将原密码覆盖；如果权限被授予给一个不存在的用户，MySQL会自动执行一条 CREATE USER语句来创建这个用户，但同时必须为该用户指定口令。

GRANT语句中的`<权限类型>`的使用说明如下：

###  1\) 授予数据库权限时，&lt;权限类型&gt;可以指定为以下值：

*  SELECT：表示授予用户可以使用 SELECT 语句访问特定数据库中所有表和视图的权限。
*  INSERT：表示授予用户可以使用 INSERT 语句向特定数据库中所有表添加数据行的权限。
*  DELETE：表示授予用户可以使用 DELETE 语句删除特定数据库中所有表的数据行的权限。
*  UPDATE：表示授予用户可以使用 UPDATE 语句更新特定数据库中所有数据表的值的权限。
*  REFERENCES：表示授予用户可以创建指向特定的数据库中的表外键的权限。
*  CREATE：表示授权用户可以使用 CREATE TABLE 语句在特定数据库中创建新表的权限。
*  ALTER：表示授予用户可以使用 ALTER TABLE 语句修改特定数据库中所有数据表的权限。
*  SHOW VIEW：表示授予用户可以查看特定数据库中已有视图的视图定义的权限。
*  CREATE ROUTINE：表示授予用户可以为特定的数据库创建存储过程和存储函数的权限。
*  ALTER ROUTINE：表示授予用户可以更新和删除数据库中已有的存储过程和存储函数的权限。
*  INDEX：表示授予用户可以在特定数据库中的所有数据表上定义和删除索引的权限。
*  DROP：表示授予用户可以删除特定数据库中所有表和视图的权限。
*  CREATE TEMPORARY TABLES：表示授予用户可以在特定数据库中创建临时表的权限。
*  CREATE VIEW：表示授予用户可以在特定数据库中创建新的视图的权限。
*  EXECUTE ROUTINE：表示授予用户可以调用特定数据库的存储过程和存储函数的权限。
*  LOCK TABLES：表示授予用户可以锁定特定数据库的已有数据表的权限。
*  ALL 或 ALL PRIVILEGES：表示以上所有权限。

###  2\) 授予表权限时，&lt;权限类型&gt;可以指定为以下值：

*  SELECT：授予用户可以使用 SELECT 语句进行访问特定表的权限。
*  INSERT：授予用户可以使用 INSERT 语句向一个特定表中添加数据行的权限。
*  DELETE：授予用户可以使用 DELETE 语句从一个特定表中删除数据行的权限。
*  DROP：授予用户可以删除数据表的权限。
*  UPDATE：授予用户可以使用 UPDATE 语句更新特定数据表的权限。
*  ALTER：授予用户可以使用 ALTER TABLE 语句修改数据表的权限。
*  REFERENCES：授予用户可以创建一个外键来参照特定数据表的权限。
*  CREATE：授予用户可以使用特定的名字创建一个数据表的权限。
*  INDEX：授予用户可以在表上定义索引的权限。
*  ALL 或 ALL PRIVILEGES：所有的权限名。

###  3\) 授予列权限时，&lt;权限类型&gt;的值只能指定为 SELECT、INSERT 和 UPDATE，同时权限的后面需要加上列名列表 column-list。

###  4\) 最有效率的权限是用户权限。

 授予用户权限时，&lt;权限类型&gt;除了可以指定为授予数据库权限时的所有值之外，还可以是下面这些值：

*  CREATE USER：表示授予用户可以创建和删除新用户的权限。
*  SHOW DATABASES：表示授予用户可以使用 SHOW DATABASES 语句查看所有已有的数据库的定义的权限。

 【实例】使用GRANT语句创建一个新的用户testUser，密码为testPwd。用户testUser对所有的数据有查询、插入权限，并授予GRANT权限。输入的 SQL 语句和执行过程如下所示。

```text
mysql> GRANT SELECT,INSERT ON *.*
    -> TO 'testUser'@'localhost'
    -> IDENTIFIED BY 'testPwd'
    -> WITH GRANT OPTION;
Query OK, 0 rows affected, 1 warning (0.05 sec)
```

 使用 SELECT 语句查询用户 testUser 的权限，如下所示。

```text
mysql> SELECT Host,User,Select_priv,Grant_priv
    -> FROM mysql.user
    -> WHERE User='testUser';
+-----------+----------+-------------+------------+
| Host      | User     | Select_priv | Grant_priv |
+-----------+----------+-------------+------------+
| localhost | testUser | Y           | Y          |
+-----------+----------+-------------+------------+
1 row in set (0.01 sec)
```

