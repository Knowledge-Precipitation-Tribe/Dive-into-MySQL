---
description: 动手学MySQL
---

# Dive-into-MySQL

![](.gitbook/assets/image%20%28135%29.png)

官网：[https://www.mysql.com/cn/](https://www.mysql.com/cn/)

## 数据库

数据库这个术语的用法很多，但就本书而言，数据库是一个以某种有组织的方式存储的数据集合。理解数据库的一种最简单的办法是将其想象为一个文件柜。此文件柜是一个存放数据的物理位置，不管数据是什么以及如何组织的。

{% hint style="info" %}
人们通常用数据库这个术语来代表他们使用的数据库软件。这是不正确的，它是引起混淆的根源。确切地说，数据库软件应称为DBMS（数据库管理系统）。数据库是通过DBMS创建和操纵的容器。数据库可以是保存在硬设备上的文件，但也可以不是。在很大程度上说，数据库究竟是文件还是别的什么东西并不重要，因为你并不直接访问数据库；你使用的是DBMS，它替你访问数据库。
{% endhint %}

## 为什么需要数据库

* 数据可以持久化存储
* 使用SQL语句，查询方便效率高
* 管理数据方便

## 关系型数据库与非关系型数据库

![](.gitbook/assets/image%20%28140%29.png)

## 数据表

在你将资料放入自己的文件柜时，并不是随便将它们扔进某个抽屉就完事了，而是在文件柜中创建文件，然后将相关的资料放入特定的文件中。

在数据库领域中，这种文件称为表。表是一种结构化的文件，可用来存储某种特定类型的数据。表可以保存顾客清单、产品目录，或者其他信息清单。

## SQL语句

* DDL：数据定义语言DDL（Data Ddefinition Language）CREATE，DROP，ALTER，主要为以上操作 即对逻辑结构等有操作的，其中包括表结构，视图和索引。
* DQL： 数据查询语言DQL（Data Query Language）SELECT，这个较为好理解 即查询操作，以select关键字。各种简单查询，连接查询等 都属于DQL。
* DML：数据操纵语言DML（Data Manipulation Language）INSERT，UPDATE，DELETE，主要为以上操作 即对数据进行操作的，对应上面所说的查询操作 DQL与DML共同构建了多数初级程序员常用的增删改查操作。而查询是较为特殊的一种 被划分到DQL中。
* DCL：数据控制功能DCL（Data Control Language）GRANT，REVOKE，COMMIT，ROLLBACK，主要为以上操作 即对数据库安全性完整性等有操作的，可以简单的理解为权限控制等。

## MySQL逻辑架构

![](.gitbook/assets/image%20%28134%29.png)

## 推荐

\[1\] [MySQL必知必会](https://book.douban.com/subject/3354490/)

\[2\] [高性能MySQL](https://book.douban.com/subject/23008813/)

\[3\] MySQL教程：[MySQL数据库学习宝典（从入门到精通）](http://c.biancheng.net/mysql/)

\[4\] [cystanford](https://github.com/cystanford)：[SQL-XMind](https://github.com/cystanford/SQL-XMind)

