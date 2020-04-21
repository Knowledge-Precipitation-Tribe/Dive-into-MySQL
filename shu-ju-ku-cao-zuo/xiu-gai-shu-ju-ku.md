# 修改数据库

如果我们在创建数据库时忘记了指定字符集可能导致后期插入中文时出现乱码的情况，所以这时就需要我们修改一下数据库的字符集。

在 MySQL 中，可以使用 `ALTER DATABASE`来修改已经被创建或者存在的数据库的相关参数。修改数据库的语法格式为：

```text
ALTER DATABASE [数据库名] { 
[ DEFAULT ] CHARACTER SET <字符集名> |
[ DEFAULT ] COLLATE <校对规则名>}
```

我们来看一下刚才创建的test\_db数据库。

![](../.gitbook/assets/image%20%2877%29.png)

可以看到它的默认字符集是latin1，现在我们将其修改为utf8。

```text
ALTER DATABASE test_db DEFAULT CHARACTER SET utf8;
```

![](../.gitbook/assets/image%20%2816%29.png)

