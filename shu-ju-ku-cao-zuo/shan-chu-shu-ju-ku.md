# 删除数据库

当数据库不再使用时应该将其删除，以确保数据库存储空间中存放的是有效数据。删除数据库是将已经存在的数据库从磁盘空间上清除，清除之后，数据库中的所有数据也将一同被删除。

在 MySQL 中，当需要删除已创建的数据库时，可以使用 **DROP DATABASE** 语句。其语法格式为：

```text
DROP DATABASE [ IF EXISTS ] <数据库名>
```

我们将刚才的db\_test数据库删除

![](../.gitbook/assets/image%20%2862%29.png)

来看一下db\_test数据库确实删除了

![](../.gitbook/assets/image%20%28125%29.png)

{% hint style="danger" %}
使用 DROP DATABASE 命令时要非常谨慎，在执行该命令后，MySQL 不会给出任何提示确认信息。DROP DATABASE 删除数据库后，数据库中存储的所有数据表和数据也将一同被删除，而且不能恢复。因此最好在删除数据库之前先将数据库进行备份。
{% endhint %}

