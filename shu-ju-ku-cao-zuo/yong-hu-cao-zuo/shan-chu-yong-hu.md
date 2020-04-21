# 删除用户

MySQL数据库中可以使用DROP USER语句来删除一个或多个用户账号以及相关的权限。

 语法格式：

```text
DROP USER <用户名1> [ , <用户名2> ]…
```

 使用DROP USER语句应该注意以下几点：

*  DROP USER语句可用于删除一个或多个MySQL账户，并撤销其原有权限。
*  使用DROP USER语句必须拥有MySQL中的MySQL数据库的DELETE权限或全局CREATE USER权限。
*  在DROP USER语句的使用中，若没有明确地给出账户的主机名，则该主机名默认为“%”。

> 注意：用户的删除不会影响他们之前所创建的表、索引或其他数据库对象，因为MySQL并不会记录是谁创建了这些对象。

 【实例】使用DROP USER语句删除用户'jack'@'localhost'。输入的SQL语句和执行过程如下所示。

```text
mysql> DROP USER 'jack'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```

 在Windows命令行工具中，使用jack和密码lion登录数据库服务器，发现登录失败，说明用户已经删除，如下所示。

```text
C:\Users\USER>mysql -h localhost -u jack -p
Enter password: ****
ERROR 1045 (28000): Access denied for user 'jack'@'localhost' (using  password: YES)
```

