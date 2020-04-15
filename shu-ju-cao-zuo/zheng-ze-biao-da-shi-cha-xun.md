# 正则表达式查询

MySQL中正式表达式通常被用来检索或替换符合某个模式的文本内容，根据指定的匹配模式匹配文中符合要求的特殊字符串。

 例如，从一个文件中提取电话号码，查找一篇文章中重复的单词或替换用户输入的敏感语汇等，这些地方都可以使用正则表达式。正则表达式强大而且灵活，常用于复杂的查询。

 MySQL 中使用 REGEXP 关键字指定正则表达式的字符匹配模式，下表列出了 REGEXP 操作符中常用的匹配列表。

|  选项 |  说明 |  例子 |  匹配值示例 |
| :--- | :--- | :--- | :--- |
|  ^ |  匹配文本的开始字符 |  '^b' 匹配以字母 b 开头 的字符串 |  book、big、banana、 bike |
|  $ |  匹配文本的结束字符 |  'st$’ 匹配以 st 结尾的字 符串 |  test、resist、persist |
|  . |  匹配任何单个字符 |  'b.t’ 匹配任何 b 和 t 之间有一个字符 |  bit、bat、but、bite |
|  \* |  匹配零个或多个在它前面的字 符 |  'f\*n’ 匹配字符 n 前面有 任意个字符 f |  fn、fan、faan、abcn |
|  + |  匹配前面的字符 1 次或多次 |  'ba+’ 匹配以 b 开头，后 面至少紧跟一个 a |  ba、bay、bare、battle |
|  &lt;字符串&gt; |  匹配包含指定字符的文本 |  'fa’ |  fan、afa、faad |
|  \[字符集合\] |  匹配字符集合中的任何一个字 符 |  '\[xz\]'匹配 x 或者 z |  dizzy、zebra、x-ray、 extra |
|  \[^\] |  匹配不在括号中的任何字符 |  '\[^abc\]’ 匹配任何不包 含 a、b 或 c 的字符串 |  desk、fox、f8ke |
|  字符串{n,} |  匹配前面的字符串至少 n 次 |  b{2} 匹配 2 个或更多 的 b |  bbb、 bbbb、 bbbbbbb |
|  字符串  {n,m} |  匹配前面的字符串至少 n 次， 至多 m 次 |  b{2,4} 匹配最少 2 个， 最多 4 个 b |  bbb、 bbbb |

##  查询以特定字符或字符串开头的记录

 字符“^”匹配以特定字符或者字符串开头的文本。

 【实例 1】在 tb\_departments 表中，查询 dept\_name 字段以字母“C”开头的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP '^C';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       1 | Computer  | 11111     | A         |
|       3 | Chinese   | 33333     | B         |
+---------+-----------+-----------+-----------+
2 rows in set (0.05 sec)
```

 在 tb\_departments 表中有两条记录的 dept\_name 字段值是以字母 C 开头的，返回结果有 2 条记录。

 【实例 2】在 tb\_departments 表中，查询 dept\_name 字段以“Ch”开头的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP '^Ch';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       3 | Chinese   | 33333     | B         |
+---------+-----------+-----------+-----------+
1 row in set (0.03 sec)
```

 只有 Chinese 是以“Ch”开头的，所以查询结果中只有 1 条记录。

##  查询以特定字符或字符串结尾的记录

 字符“$”匹配以特定字符或者字符串结尾的文本。

 【实例 3】在 tb\_departments 表中，查询 dept\_name 字段以字母“y”结尾的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP 'y$';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       4 | Economy   | 44444     | B         |
|       5 | History   | 55555     | B         |
+---------+-----------+-----------+-----------+
2 rows in set (0.00 sec)
```

 在 tb\_departments 表中有两条记录的 dept\_name 字段值是以字母 y 结尾的，返回结果有 2 条记录。

 【实例 4】在 tb\_departments 表中，查询 dept\_name 字段以“my”结尾的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP 'my$';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       4 | Economy   | 44444     | B         |
+---------+-----------+-----------+-----------+
1 row in set (0.00 sec)
```

 只有 Economy 是以“my”结尾的，所以查询结果中只有 1 条记录。

##  用符号“.”代替字符串中的任意一个字符

 【实例 5】在 tb\_departments 表中，查询 dept\_name 字段值包含字母“o”与字母“y”，且两个字母之间只有一个字母的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP 'o.y';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       4 | Economy   | 44444     | B         |
|       5 | History   | 55555     | B         |
+---------+-----------+-----------+-----------+
2 rows in set (0.00 sec)
```

 查询语句中“o.y”指定匹配字符中要有字母 o 和 y，且两个字母之间包含单个字符，并不限定匹配的字符的位置和所在查询字符串的总长度，因此 Economy 和 History 都符合匹配条件。

##  使用“\*”和“+”来匹配多个字符

 星号“\*”匹配前面的字符任意多次，包括 0 次。加号“+”匹配前面的字符至少一次。

 【实例 6】在 tb\_departments 表中，查询 dept\_name 字段值包含字母“C”，且“C”后面出现字母“h”的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP '^Ch*';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       1 | Computer  | 11111     | A         |
|       3 | Chinese   | 33333     | B         |
+---------+-----------+-----------+-----------+
2 rows in set (0.00 sec)
```

 星号“\*”可以匹配任意多个字符，Computer 中字母 C 后面并没有出现字母 h，但是也满足匹配条件。

 【实例 7】在 tb\_departments 表中，查询 dept\_name 字段值包含字母“C”，且“C”后面出现字母“h”至少一次的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP '^Ch+';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       3 | Chinese   | 33333     | B         |
+---------+-----------+-----------+-----------+
1 row in set (0.00 sec)
```

 “h+”匹配字母“h”至少一次，只有 Chinese 满足匹配条件。

##  匹配指定字符串

 正则表达式可以匹配指定字符串，只要这个字符串在查询文本中即可，若要匹配多个字符串，则多个字符串之间使用分隔符“\|”隔开。

 【实例 8】在 tb\_departments 表中，查询 dept\_name 字段值包含字符串“in”的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP 'in';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       3 | Chinese   | 33333     | B         |
+---------+-----------+-----------+-----------+
1 row in set (0.00 sec)
```

 可以看到，dept\_name 字段的 Chinese 中包含字符串“in”，满足匹配条件。

 【实例 9】在 tb\_departments 表中，查询 dept\_name 字段值包含字符串“in”或者“on”的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP 'in|on';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       3 | Chinese   | 33333     | B         |
|       4 | Economy   | 44444     | B         |
+---------+-----------+-----------+-----------+
2 rows in set (0.00 sec)
```

 可以看到，dept\_name 字段的 Chinese 中包含字符串“in”，Economy 中包含字符串“on”，满足匹配条件。

> 提示：LIKE 运算符也可以匹配指定的字符串，但与 REGEXP 不同，LIKE 匹配的字符串如果在文本中间出现，就找不到它，相应的行也不会返回。而 REGEXP 在文本内进行匹配，如果被匹配的字符串在文本中出现，REGEXP 将会找到它，相应的行也会被返回。

##  匹配指定字符串中的任意一个

 方括号“\[\]”指定一个字符集合，只匹配其中任何一个字符，即为所查找的文本。

 【实例 10】在 tb\_departments 表中，查询 dept\_name 字段值包含字母“o”或者“e”的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP '[io]';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       1 | Computer  | 11111     | A         |
|       3 | Chinese   | 33333     | B         |
|       4 | Economy   | 44444     | B         |
|       5 | History   | 55555     | B         |
+---------+-----------+-----------+-----------+
4 rows in set (0.00 sec)
```

 从查询结果可以看到，所有返回的记录的 dept\_name 字段的值中都包含字母 o 或者 e，或者两个都有。

 方括号“\[\]”还可以指定数值集合。

 【实例 11】在 tb\_departments 表中，查询 dept\_call 字段值中包含 1、2 或者 3 的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_call REGEXP '[123]';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       1 | Computer  | 11111     | A         |
|       2 | Math      | 22222     | A         |
|       3 | Chinese   | 33333     | B         |
+---------+-----------+-----------+-----------+
3 rows in set (0.00 sec)
```

 查询结果中，dept\_call 字段值中有 1、2、3 三个数字中的一个即为匹配记录字段。

 匹配集合“\[123\]”也可以写成“\[1-3\]”，即指定集合区间。例如，“\[a-z\]”表示集合区间为a~z的字母，“\[0-9\]”表示集合区间为所有数字。

##  匹配指定字符以外的字符

 “\[^字符集合\]”匹配不在指定集合中的任何字符。

 【实例 12】在 tb\_departments 表中，查询 dept\_name 字段值包含字母 a~t 以外的字符的记录，输入的 SQL 语句和执行结果如下所示。

```text
mysql> SELECT * FROM tb_departments
    -> WHERE dept_name REGEXP '[^a-t]';
+---------+-----------+-----------+-----------+
| dept_id | dept_name | dept_call | dept_type |
+---------+-----------+-----------+-----------+
|       1 | Computer  | 11111     | A         |
|       4 | Economy   | 44444     | B         |
|       5 | History   | 55555     | B         |
+---------+-----------+-----------+-----------+
3 rows in set (0.00 sec)
```

 返回记录中的 dept\_name 字段值中包含了指定字母和数字以外的值，如 u、y 等，这些字母均不在 a～t 中，满足匹配条件。

