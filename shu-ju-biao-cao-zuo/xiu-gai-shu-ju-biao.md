# 修改数据表

在 MySQL 中可以使用 **ALTER TABLE** 语句来改变原有表的结构，例如增加或删减列、创建或取消索引、更改原有列类型、重新命名列或表等。

```text
ALTER TABLE <表名> [修改选项]
```

修改选项的语法格式如下：

* ADD COLUMN &lt;列名&gt; &lt;类型&gt;
* CHANGE COLUMN &lt;旧列名&gt; &lt;新列名&gt; &lt;新列类型&gt;
* ALTER COLUMN &lt;列名&gt; { SET DEFAULT &lt;默认值&gt; \| DROP DEFAULT }
* MODIFY COLUMN &lt;列名&gt; &lt;类型&gt;
* DROP COLUMN &lt;列名&gt;
* RENAME TO &lt;新表名&gt;

### 添加字段

随着业务的变化，可能需要在已经存在的表中添加新的字段，一个完整的字段包括字段名、数据类型、完整性约束。添加字段的语法格式如下：

```text
ALTER TABLE <表名> ADD <新字段名> <数据类型> [约束条件] [FIRST|AFTER 已存在的字段名]；
```

`新字段名`为需要添加的字段的名称；`FIRST` 为可选参数，其作用是将新添加的字段设置为表的第一个字段；`AFTER` 为可选参数，其作用是将新添加的字段添加到指定的`已存在的字段名`的后面。

使用 ALTER TABLE 修改表 tb\_emp1 的结构，在表的第一列添加一个 int 类型的字段 col1。

```text
ALTER TABLE tb_emp1 ADD COLUMN col1 INT FIRST;
```

![](../.gitbook/assets/image%20%2880%29.png)

使用 ALTER TABLE 修改表 tb\_emp1 的结构，在一列 name 后添加一个 int 类型的字段 col2。

```text
ALTER TABLE tb_emp1 ADD COLUMN col2 INT AFTER name;
```

![](../.gitbook/assets/image%20%2887%29.png)

### 修改字段数据类型

修改字段的数据类型就是把字段的数据类型转换成另一种数据类型。在 MySQL 中修改字段数据类型的语法规则如下：

```text
ALTER TABLE <表名> MODIFY <字段名> <数据类型>
```

使用 ALTER TABLE 修改表 tb\_emp1 的结构，将 name 字段的数据类型由 VARCHAR\(22\) 修改成 VARCHAR\(30\)。

```text
ALTER TABLE tb_emp1 MODIFY name VARCHAR(30);
```

![](../.gitbook/assets/image%20%2879%29.png)

### 删除字段

删除字段是将数据表中的某个字段从表中移除，语法格式如下：

```text
ALTER TABLE <表名> DROP <字段名>；
```

使用 ALTER TABLE 修改表 tb\_emp1 的结构，删除 col2 字段。

```text
ALTER TABLE tb_emp1 DROP col2;
```

![](../.gitbook/assets/image%20%2828%29.png)

### 修改字段名称

MySQL 中修改表字段名的语法规则如下：

```text
ALTER TABLE <表名> CHANGE <旧字段名> <新字段名> <新数据类型>；
```

使用 ALTER TABLE 修改表 tb\_emp1 的结构，将 col1 字段名称改为 col3，同时将数据类型变为 CHAR\(30\)。

```text
ALTER TABLE tb_emp1 CHANGE col1 col3 CHAR(30);
```

![](../.gitbook/assets/image%20%2852%29.png)

### 修改表名

MySQL 通过 ALTER TABLE 语句来实现表名的修改，语法规则如下：

```text
ALTER TABLE <旧表名> RENAME [TO] <新表名>；
```

使用 ALTER TABLE 将数据表 tb\_emp1 改名为 tb\_emp2。

```text
ALTER TABLE tb_emp1 RENAME TO tb_emp2;
```

![](../.gitbook/assets/image%20%2859%29.png)

