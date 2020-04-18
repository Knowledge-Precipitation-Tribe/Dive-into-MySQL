# 查询数据去重

我们在查询数据时可能某些列存在重复数据，但是我们想要分析数据，每种数据返回一种即可，这是就要用到去重操作。

```text
SELECT DISTINCT <字段名> FROM <表名>;
```

默认查询age字段

```text
SELECT age FROM tb_students_info;
```

![](../.gitbook/assets/image%20%2894%29.png)

使用去重操作

```text
SELECT DISTINCT age FROM tb_students_info;
```

![](../.gitbook/assets/image%20%2848%29.png)

