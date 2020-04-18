# 创建用户

在对 MySQL 的日常管理和实际操作中，为了避免用户恶意冒名使用 root 账号控制数据库，通常需要创建一系列具备适当权限的账号，应该尽可能地不用或少用 root 账号登录系统，以此来确保数据的安全访问。

##  创建用户

 可以使用 CREATE USER 语句来创建一个或多个 MySQL 账户，并设置相应的口令。

 语法格式：

```text
CREATE USER <用户名> [ IDENTIFIED ] BY [ PASSWORD ] <口令>
```

 语法说明如下：

###  1\) &lt;用户名&gt;

 指定创建用户账号，格式为 'user\_name'@'host\_name'。这里`user_name`是用户名，`host_name`为主机名，即用户连接 MySQL 时所在主机的名字。若在创建的过程中，只给出了账户的用户名，而没指定主机名，则主机名默认为“%”，表示一组主机。

###  2\) PASSWORD

 可选项，用于指定散列口令，即若使用明文设置口令，则需忽略`PASSWORD`关键字；若不想以明文设置口令，且知道 PASSWORD\(\) 函数返回给密码的散列值，则可以在口令设置语句中指定此散列值，但需要加上关键字`PASSWORD`。

###  3\) IDENTIFIED BY子句

 用于指定用户账号对应的口令，若该用户账号无口令，则可省略此子句。

###  4\) &lt;口令&gt;

 指定用户账号的口令，在`IDENTIFIED BY`关键字或`PASSWOED`关键字之后。给定的口令值可以是只由字母和数字组成的明文，也可以是通过 PASSWORD\(\) 函数得到的散列值。

 使用 CREATE USER 语句应该注意以下几点：

*  如果使用 CREATE USER 语句时没有为用户指定口令，那么 MySQL 允许该用户可以不使用口令登录系统，然而从安全的角度而言，不推荐这种做法。
*  使用 CREATE USER 语句必须拥有 MySQL 中 MySQL 数据库的 INSERT 权限或全局 CREATE USER 权限。
*  使用 CREATE USER 语句创建一个用户账号后，会在系统自身的 MySQL 数据库的 user 表中添加一条新记录。若创建的账户已经存在，则语句执行时会出现错误。
*  新创建的用户拥有的权限很少。他们可以登录 MySQL，只允许进行不需要权限的操作，如使用 SHOW 语句查询所有存储引擎和字符集的列表等。

 如果两个用户具有相同的用户名和不同的主机名，MySQL 会将他们视为不同的用户，并允许为这两个用户分配不同的权限集合。

 【实例 1】使用 CREATE USER 创建一个用户，用户名是 james，密码是 tiger，主机是 localhost。输入的 SQL 语句和执行过程如下所示。

```text
mysql> CREATE USER 'james'@'localhost'
    -> IDENTIFIED BY 'tiger';
Query OK, 0 rows affected (0.12 sec)
```

 在 Windows 命令行工具中，使用新创建的用户 james 和密码 tiger 登录数据库服务器，如下所示。

```text
C:\Users\USER>mysql -h localhost -u james -p
Enter password: *****
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.7.20-log MySQL Community Server (GPL)
Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```



