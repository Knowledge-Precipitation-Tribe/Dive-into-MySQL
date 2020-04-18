# 修改用户

在 MySQL 中，我们可以使用 **RENAME USER** 语句修改一个或多个已经存在的用户账号。

 语法格式如下：

```text
RENAME USER <旧用户> TO <新用户>
```

 其中：

*  &lt;旧用户&gt;：系统中已经存在的 MySQL 用户账号。
*  &lt;新用户&gt;：新的 MySQL 用户账号。

 使用 RENAME USER 语句时应注意以下几点：

*  RENAME USER 语句用于对原有的 MySQL 用户进行重命名。
*  若系统中旧账户不存在或者新账户已存在，该语句执行时会出现错误。
*  使用 RENAME USER 语句，必须拥有 mysql 数据库的 UPDATE 权限或全局 CREATE USER 权限。

##  例 1

 使用 RENAME USER 语句将用户名 test1 修改为 testUser1，主机是 localhost。SQL 语句和执行过程如下。

```text
mysql> RENAME USER 'test1'@'localhost'
    -> TO 'testUser1'@'localhost';
Query OK, 0 rows affected (0.03 sec)
```

 在 cmd 命令行工具中，使用 testUser1 用户登录数据库服务器，如下所示。

```text
C:\Users\USER>mysql -h localhost -u testUser1 -p
Enter password: *****
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 7
Server version: 5.7.20-log MySQL Community Server (GPL)
Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

