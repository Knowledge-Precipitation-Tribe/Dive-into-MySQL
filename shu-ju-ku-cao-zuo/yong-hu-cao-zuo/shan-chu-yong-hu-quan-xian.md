# 删除用户权限

MySQL 数据库中可以使用 REVOKE 语句删除一个用户的权限，此用户不会被删除。

 语法格式有两种形式，如下所示：

##  1\) 第一种：

```text
REVOKE <权限类型> [ ( <列名> ) ] [ , <权限类型> [ ( <列名> ) ] ]…
ON <对象类型> <权限名> FROM <用户1> [ , <用户2> ]…
```

##  2\) 第二种：

```text
REVOKE ALL PRIVILEGES, GRANT OPTION
FROM user <用户1> [ , <用户2> ]…
```

 语法说明如下：

*  REVOKE 语法和 GRANT 语句的语法格式相似，但具有相反的效果。
*  第一种语法格式用于回收某些特定的权限。
*  第二种语法格式用于回收特定用户的所有权限。
*  要使用 REVOKE 语句，必须拥有 MySQL 数据库的全局 CREATE USER 权限或 UPDATE 权限。

 【实例】使用 REVOKE 语句取消用户 testUser 的插入权限，输入的 SQL 语句和执行过程如下所示。

```text
mysql> REVOKE INSERT ON *.*
    -> FROM 'testUser'@'localhost';
Query OK, 0 rows affected (0.00 sec)
mysql> SELECT Host,User,Select_priv,Insert_priv,Grant_priv
    -> FROM mysql.user
    -> WHERE User='testUser';
+-----------+----------+-------------+-------------+------------+
| Host      | User     | Select_priv | Insert_priv | Grant_priv |
+-----------+----------+-------------+-------------+------------+
| localhost | testUser | Y           | N           | Y          |
+-----------+----------+-------------+-------------+------------+
1 row in set (0.00 sec)
```

