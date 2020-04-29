# 创建数据库

在MySQL中可以使用`CREATE DATABASE`语句创建数据库，语法格式

```text
CREATE DATABASE [IF NOT EXISTS] <数据库名> [[DEFAULT] CHARACTER SET <字符集名>] [[DEFAULT] COLLATE <校对规则名>];
```

### 创建数据库-简单版本

```text
CREATE DATABASE test_db
```

![](../.gitbook/assets/image%20%2887%29.png)

{% hint style="info" %}
数据库的名称不能重复
{% endhint %}

使用`IF NOT EXISTS`来避免创建数据库错误。

![](../.gitbook/assets/image%20%28126%29.png)

### 创建数据库时指定数据集

```text
CREATE DATABASE IF NOT EXISTS test_db_char DEFAULT CHARACTER SET utf8;
```

![](../.gitbook/assets/image%20%2873%29.png)

可以使用`SHOW CREATE DATABASE`查看 test\_db\_char 数据库的定义声明。

```text
SHOW CREATE DATABASE test_db_char;
```

![](../.gitbook/assets/image%20%2888%29.png)

