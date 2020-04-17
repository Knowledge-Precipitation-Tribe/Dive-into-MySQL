# 创建视图

创建视图是指在已经存在的 MySQL 数据库表上建立视图。视图可以建立在一张表中，也可以建立在多张表中。

##  基本语法

 可以使用 CREATE VIEW 语句来创建视图。

 语法格式如下：

```text
CREATE VIEW <视图名> AS <SELECT语句>
```

 语法说明如下。

*  `<视图名>`：指定视图的名称。该名称在数据库中必须是唯一的，不能与其他表或视图同名。
*  `<SELECT语句>`：指定创建视图的 SELECT 语句，可用于查询多个基础表或源视图。

 对于创建视图中的 SELECT 语句的指定存在以下限制：

*  用户除了拥有 CREATE VIEW 权限外，还具有操作中涉及的基础表和其他视图的相关权限。
*  SELECT 语句不能引用系统或用户变量。
*  SELECT 语句不能包含 FROM 子句中的子查询。
*  SELECT 语句不能引用预处理语句参数。

 视图定义中引用的表或视图必须存在。但是，创建完视图后，可以删除定义引用的表或视图。可使用 CHECK TABLE 语句检查视图定义是否存在这类问题。

 视图定义中允许使用 ORDER BY 语句，但是若从特定视图进行选择，而该视图使用了自己的 ORDER BY 语句，则视图定义中的 ORDER BY 将被忽略。

 视图定义中不能引用 TEMPORARY 表（临时表），不能创建 TEMPORARY 视图。

 WITH CHECK OPTION 的意思是，修改视图时，检查插入的数据是否符合 WHERE 设置的条件。

##  创建基于单表的视图

 MySQL 可以在单个数据表上创建视图。

 查看 test\_db 数据库中的 tb\_students\_info 表的数据，如下所示。

```text
SELECT t.* FROM test_db.tb_students_info t
```

![](../../.gitbook/assets/image%20%2825%29.png)

 【实例 1】在 tb\_students\_info 表上创建一个名为 view\_students\_info 的视图，输入的 SQL 语句和执行结果如下所示。

```text
CREATE VIEW view_students_info AS SELECT * FROM tb_students_info;
```

```text
SELECT * FROM view_students_info;
```

![](../../.gitbook/assets/image%20%2862%29.png)

 默认情况下，创建的视图和基本表的字段是一样的，也可以通过指定视图字段的名称来创建视图。

 【实例 2】在 tb\_students\_info 表上创建一个名为 v\_students\_info 的视图，输入的 SQL 语句和执行结果如下所示。

```text
CREATE VIEW v_students_info
    (s_id,s_name,d_id,s_age,s_sex,s_height,s_date)
    AS SELECT id,name,deptId,age,sex,height,login_data
    FROM tb_students_info;
```

![](../../.gitbook/assets/image%20%2879%29.png)

 可以看到，view\_students\_info 和 v\_students\_info 两个视图中的字段名称不同，但是数据却相同。因此，在使用视图时，可能用户不需要了解基本表的结构，更接触不到实际表中的数据，从而保证了数据库的安全。

##  创建基于多表的视图

 MySQL 中也可以在两个以上的表中创建视图，使用 CREATE VIEW 语句创建。

我们在创建一个tb\_class表，并向内插入数据

```text
CREATE TABLE tb_class(
    id INT PRIMARY KEY,
    name VARCHAR(11)
);

INSERT INTO tb_class VALUES (1, '1班');
INSERT INTO tb_class VALUES (3, '3班');

SELECT * FROM tb_class;
```

![](../../.gitbook/assets/image%20%2867%29.png)

 【实例 3】在表 tb\_student\_info 和表 tb\_class上创建视图 v\_student，输入的 SQL 语句和执行结果如下所示。

```text
CREATE VIEW v_student (s_name, s_age, s_sex, c_name)
    AS SELECT  s.name, s.age, s.sex, c.name FROM tb_students_info s, tb_class c
    WHERE s.id = c.id;
```

![](../../.gitbook/assets/image%20%2871%29.png)

 通过这个视图可以很好地保护基本表中的数据。视图中包含 s\_name、s\_age、s\_sex字段对应 tb\_students\_info 表中的 字段，c\_name 字段对应 tb\_class 表中的 name 字段。

##  查询视图

 视图一经定义之后，就可以如同查询数据表一样，使用 SELECT 语句查询视图中的数据，语法和查询基础表的数据一样。

 视图用于查询主要应用在以下几个方面：

*  使用视图重新格式化检索出的数据。
*  使用视图简化复杂的表连接。
*  使用视图过滤数据。

 DESCRIBE 可以用来查看视图，语法如下：

```text
DESCRIBE 视图名；
```

 【实例 4】通过 DESCRIBE 语句查看视图 v\_students\_info 的定义，输入的 SQL 语句和执行结果如下所示。

```text
DESCRIBE v_student;
```

![](../../.gitbook/assets/image%20%282%29.png)

> 注意：DESCRIBE 一般情况下可以简写成 DESC，输入这个命令的执行结果和输入 DESCRIBE 是一样的。

