# 类型变量

## 定义变量方式

### 直接赋值

使用set或select直接赋值，变量名以 @ 开头. 例如:

```text
set @var=1; 
```

可以在一个会话的任何地方声明，作用域是整个会话，称为用户变量。

### DECLARE声明

以 DECLARE 关键字声明的变量，只能在存储过程中使用，称为存储过程变量，例如： 

```text
DECLARE var1 INT DEFAULT 0; 
```

主要用在存储过程中，或者是给存储传参数中。

### 两者的区别

 在调用存储过程时，以DECLARE声明的变量都会被初始化为 NULL。而会话变量（即@开头的变量）则不会被再初始化，在一个会话内，只须初始化一次，之后在会话内都是对上一次计算的结果，就相当于在是这个会话内的全局变量。

## 局部变量

局部变量一般用在sql语句块中，比如存储过程的begin/end。其作用域仅限于该语句块，在该语句块执行完毕后，局部变量就消失了。declare语句专门用于定义局部变量，可以使用default来说明默认值。set语句是设置不同类型的变量，包括会话变量和全局变量。 局部变量定义语法形式

```sql
DECLARE var_name [, var_name]... data_type [ DEFAULT value ];
```

例如在begin/end语句块中添加如下一段语句，接受函数传进来的a/b变量然后相加，通过set语句赋值给c变量。set语句语法形式`SET var_name=expr [, var_name=expr]...;` set语句既可以用于局部变量的赋值，也可以用于用户变量的申明并赋值。

```sql
DECLARE c int DEFAULT 0;
SET c=a+b;
SELECT c AS C;
```

或者用select …. into…形式赋值

```sql
select into 语句句式：SELECT col_name[,...] INTO var_name[,...] table_expr [WHERE...];
```

例子

```sql
DECLARE v_employee_name VARCHAR(100);
DECLARE v_employee_salary DECIMAL(8,4);

SELECT employee_name, employee_salary
INTO v_employee_name, v_employee_salary
FROM employees
WHERE employee_id=1;
```

## 用户变量

mysql中用户变量不用事前申明，在用的时候直接用“@变量名”使用就可以了。  
第一种用法：`set @num=1; 或set @num:=1;` //这里要使用set语句创建并初始化变量，直接使用@num变量  
第二种用法：`select @num:=1; 或 select @num:=字段名 from 表名 where ……`，  
**select语句一般用来输出用户变量，比如select @变量名,用于输出数据源不是表格的数据。**  
注意上面两种赋值符号，使用set时可以用“=”或“:=”，但是使用select时必须用“:=赋值”

**用户变量的生命周期与数据库连接**有关，在连接中声明的变量会一直存活到到数据库连接断开，数据库连接断开后变量就会消失。

* 在此连接中声明的变量无法在另一连接中使用。
* 用户变量的变量名的形式为@varname的形式。
* 名字必须以@开头。
* 声明变量的时候需要使用set语句，比如下面的语句声明了一个名为@a的变量。

```sql
set @a = 1;
```

**声明一个名为@a的变量，并将它赋值为1，mysql里面的变量是不严格限制数据类型的，它的数据类型根据你赋给它的值而随时变化** 。（SQL SERVER中使用declare语句声明变量，且严格限制数据类型。）我们还可以使用select 语句为变量赋值 。 比如：

```sql
set @name = '';
select @name:=password from user limit 0,1;
#从数据表中获取一条记录password字段的值给@name变量。在执行后输出到查询结果集上面。
```

注意等于号前面有一个冒号，后面的limit 0,1是用来限制返回结果的，表示可以是0或1个。如果直接写：`select @name:=password from user;`如果这个查询返回多个值的话，那@name变量的值就是最后一条记录的password字段的值 。

转载并加以整理：[https://blog.csdn.net/JQ\_AK47/article/details/52087484](https://blog.csdn.net/JQ_AK47/article/details/52087484)



