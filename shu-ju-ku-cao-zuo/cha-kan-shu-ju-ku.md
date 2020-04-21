# 查看数据库

数据库可以看作是超市里的水果区，每一个水果区里面有着不同的筐装着不同水果，这个筐就对应着数据表。可以发现每个水果区也就是数据库的名字都应该是有含义的，这样可以看出每个数据库用来存档着哪些数据。

在MySQL中，可以使用SHOW DATABASE语句来查看当前用户权限下的数据库。查看数据库的语法格式为：

```text
SHOW DATABASES [LIKE '数据库名'];
```

### 查看所有数据库

![](../.gitbook/assets/image%20%2854%29.png)

### 使用LIKE

我们首先创建三个数据库分别为：test\_db, db\_test, db\_test\_db。

![](../.gitbook/assets/image%20%2871%29.png)

#### 查看与test\_db完全匹配的数据库

```text
SHOW DATABASES LIKE 'test_db';
```

![](../.gitbook/assets/image%20%2868%29.png)

#### 查看名字中包含test的数据库

```text
SHOW DATABASES LIKE '%test%';
```

{% hint style="info" %}
在mysql中使用%来匹配任意字符
{% endhint %}

![](../.gitbook/assets/image%20%2870%29.png)

#### 查看以db开头的数据库

```text
SHOW DATABASES LIKE 'db%';
```

![](../.gitbook/assets/image%20%2838%29.png)

