# 触发器简介

MySQL 数据库中触发器是一个特殊的存储过程，不同的是执行存储过程要使用 CALL 语句来调用，而触发器的执行不需要使用 CALL 语句来调用，也不需要手工启动，只要一个预定义的事件发生就会被 MySQL自动调用。

 引发触发器执行的事件一般如下：

*  增加一条学生记录时，会自动检查年龄是否符合范围要求。
*  每当删除一条学生信息时，自动删除其成绩表上的对应记录。
*  每当删除一条数据时，在数据库存档表中保留一个备份副本。

 触发程序的优点如下：

*  触发程序的执行是自动的，当对触发程序相关表的数据做出相应的修改后立即执行。
*  触发程序可以通过数据库中相关的表层叠修改另外的表。
*  触发程序可以实施比 FOREIGN KEY 约束、CHECK 约束更为复杂的检查和操作。

 触发器与表关系密切，主要用于保护表中的数据。特别是当有多个表具有一定的相互联系的时候，触发器能够让不同的表保持数据的一致性。

 在 MySQL 中，只有执行 INSERT、UPDATE 和 DELETE 操作时才能激活触发器。

 在实际使用中，MySQL 所支持的触发器有三种：INSERT 触发器、UPDATE 触发器和 DELETE 触发器。

##  1\) INSERT 触发器

 在 INSERT 语句执行之前或之后响应的触发器。

 使用 INSERT 触发器需要注意以下几点：

*  在 INSERT 触发器代码内，可引用一个名为 NEW（不区分大小写）的虚拟表来访问被插入的行。
*  在 BEFORE INSERT 触发器中，NEW 中的值也可以被更新，即允许更改被插入的值（只要具有对应的操作权限）。
*  对于 AUTO\_INCREMENT 列，NEW 在 INSERT 执行之前包含的值是 0，在 INSERT 执行之后将包含新的自动生成值。

##  2\) UPDATE 触发器

 在 UPDATE 语句执行之前或之后响应的触发器。

 使用 UPDATE 触发器需要注意以下几点：

*  在 UPDATE 触发器代码内，可引用一个名为 NEW（不区分大小写）的虚拟表来访问更新的值。
*  在 UPDATE 触发器代码内，可引用一个名为 OLD（不区分大小写）的虚拟表来访问 UPDATE 语句执行前的值。
*  在 BEFORE UPDATE 触发器中，NEW 中的值可能也被更新，即允许更改将要用于 UPDATE 语句中的值（只要具有对应的操作权限）。
*  OLD 中的值全部是只读的，不能被更新。

> 注意：当触发器设计对触发表自身的更新操作时，只能使用 BEFORE 类型的触发器，AFTER 类型的触发器将不被允许。

##  3\) DELETE 触发器

 在 DELETE 语句执行之前或之后响应的触发器。

 使用 DELETE 触发器需要注意以下几点：

*  在 DELETE 触发器代码内，可以引用一个名为 OLD（不区分大小写）的虚拟表来访问被删除的行。
*  OLD 中的值全部是只读的，不能被更新。

 总体来说，触发器使用的过程中，MySQL 会按照以下方式来处理错误。

 若对于事务性表，如果触发程序失败，以及由此导致的整个语句失败，那么该语句所执行的所有更改将回滚；对于非事务性表，则不能执行此类回滚，即使语句失败，失败之前所做的任何更改依然有效。

 若 BEFORE 触发程序失败，则 MySQL 将不执行相应行上的操作。

 若在 BEFORE 或 AFTER 触发程序的执行过程中出现错误，则将导致调用触发程序的整个语句失败。

 仅当 BEFORE 触发程序和行操作均已被成功执行，MySQL 才会执行AFTER触发程序。
